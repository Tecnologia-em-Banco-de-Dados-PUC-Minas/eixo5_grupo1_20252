# Mortalidade — Conclusões

## 1º Resultado

- `select(...)` exibe colunas **do fluxo ambulatorial** (`nome_procedimento`, `valor_procedimento`) mesmo sendo um pipeline de **mortalidade**.
- Registros de 2022 com `MUNICÍPIO FORA DE MG`.

**Conclusões**
- **Inconsistência de schema/seleção** (provável “copiar-e-colar” do ambulatorial): a amostra não reflete as colunas específicas de mortalidade (ex.: `qtde_Obitos`).
- Presença de categoria **“fora do escopo”** (fora de MG) pode distorcer estatísticas municipais e eleva cardinalidade.


## 2º Resultado

- `df_agg` agrega por `(ano, nome_municipio, faixa_etaria, cid10)` e cria `prop_faixa_etaria = qtde_Obitos / total_ano`.
- `total_ano` é somado **apenas por ano** (global), não por município.

**Conclusões**
- A proporção **não captura estrutura etária local**: mistura todos os municípios do ano, diluindo o indicador e reduzindo sinal preditivo.
- Valores de proporção muito pequenos (na ordem de 1e-6) denunciam **denominador global**.


## 3º Resultado

- `prop_60plus` ~ 0.299… repetido em diferentes linhas, sugerindo **pouca variação** por (ano, município) no exemplo mostrado.
- Cálculo de idosos via **`idade_media >= 60`** no nível agregado.

**Conclusões**
- Usar `idade_media >= 60` em agregados pode **subestimar/superestimar** a participação idosa quando há mistura etária dentro do grupo.
- A pouca variação indica que a feature pode estar **mal definida** para capturar heterogeneidade local.


## 4º Resultado

**Conclusões**
- **Vazamento de alvo (target leakage)**: em `numeric_features` foi incluída **`qtde_Obitos`**, que é a **própria variável alvo**.  
  → Explica o **R² ~ 1** na Linear Regression e **infla** o desempenho de RF/GBT.
- Além disso, `QTDE_OBITOS` é uma variável **de contagem**; modelos e métricas contínuas podem não ser os mais adequados.


## 5º Resultado

- `nome_municipio_vec` domina (≈ 0.44); `cid10_vec` e `faixa_etaria_vec` com importâncias menores; `qtde_Obitos` aparece com peso (>0), e `prop_60plus` é muito baixo.

**Conclusões**
- A presença de **`qtde_Obitos` como feature** invalida a interpretação das importâncias (leakage).
- O vetor de nomes (`feature_names = assembler_inputs`) **não expande one-hot**: dezenas/centenas de dummies são **colapsadas** em um único rótulo (ex.: `nome_municipio_vec`), criando **falsa dominância**.



## 🛠️ Próximos Passos

### Dados e Limpeza
- [ ] Ajustar `df.select(...)` para **colunas de mortalidade** (remover campos do ambulatorial).
- [ ] Decidir tratamento para **“MUNICÍPIO FORA DE MG”** (excluir, OUTROS, ou segmentar análise).
- [ ] Normalizar nomes de municípios (acentos, casing, trims) e CIDs (mapeamento/agrupamento).

### Engenharia de Variáveis
- [ ] Recalcular `prop_faixa_etaria` **por (ano, nome_municipio)**:  
  `total_ano_mun = Σ qtde_Obitos (ano, município)`  
  `prop_faixa_etaria_mun = qtde_Obitos / total_ano_mun`
- [ ] Recalcular `prop_60plus` **via faixas etárias idosas** (60–69/70–79/80+) por **(ano, município)**.
- [ ] Considerar variáveis de **tendência e sazonalidade** (lags de óbitos por município, médias móveis, dummies sazonais).

### Modelagem e Avaliação
- [ ] **Remover `qtde_Obitos` das features** (eliminar leakage).
- [ ] Trocar/experimentar com **GLM Poisson/NegBin** (link log) para contagens; ou **modelar `log1p(qtde_Obitos)`** com RF/GBT.
- [ ] **Validação temporal** (treino ≤ 2021/2022, teste > 2021/2022) e **backtesting** por múltiplas janelas.
- [ ] Reportar **RMSE, MAE, MAPE** e, para Poisson/GLM, **deviance** e **pseudo-R²**.

### Importância e Explicabilidade
- [ ] **Expandir nomes one-hot** e **agrupar importâncias** por variável original.
- [ ] Calcular **Permutation Importance** no **teste** (pós-correções) e **parciais de dependência** para as top features.

---

## 🔧 Esboço de correções (ideia de código)
```python
# --- Proporção por município ---
total_ano_mun = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_Obitos").alias("total_ano_mun"))

df_agg = df_agg.join(total_ano_mun, ["ano", "nome_municipio"]) \
    .withColumn("prop_faixa_etaria_mun", F.col("qtde_Obitos") / F.col("total_ano_mun"))

# --- Idosos por faixas (não por idade média) ---
faixas_idosas = ["60–69", "70–79", "80+"]  # ou consolidar em "60+"
idosos = (df_agg
    .filter(F.col("faixa_etaria").isin(faixas_idosas))
    .groupBy("ano", "nome_municipio")
    .agg(F.sum("qtde_Obitos").alias("qtde_60plus")))

total = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_Obitos").alias("qtde_total"))

prop_idosos = idosos.join(total, ["ano", "nome_municipio"]) \
    .withColumn("prop_60plus", F.col("qtde_60plus") / F.col("qtde_total"))

df_ml = (df_agg
    .join(prop_idosos.select("ano", "nome_municipio", "prop_60plus"),
          ["ano", "nome_municipio"], "left")
    .fillna({"prop_60plus": 0}))

# --- Features sem leakage ---
categorical_features = ["nome_municipio", "faixa_etaria", "cid10"]
numeric_features = ["idade_media", "prop_faixa_etaria_mun", "prop_60plus"]  # (removido: qtde_Obitos)

# --- Modelos: opção 1 (GLM Poisson) ---
from pyspark.ml.regression import GeneralizedLinearRegression
glm = GeneralizedLinearRegression(family="poisson", link="log",
                                  labelCol="qtde_Obitos", featuresCol="features")
# montar pipeline com indexers/encoders + assembler (sem scaler)

# --- Modelos: opção 2 (RF/GBT em log-contagem) ---
# label_log = log1p(qtde_Obitos) -> treinar e avaliar revertendo com expm1 nas previsões

