# Internações — Conclusões

## 1º Resultado

- Colunas exibidas incluem `nome_procedimento` e `valor_procedimento` (típicas do **ambulatorial**), apesar de o escopo ser **internações**.
- Mesmos valores repetidos em `valor_internacoes` (ex.: `131348`) em múltiplas faixas.

**Conclusões**
- **Inconsistência de schema/seleção**: o `select(...)` parece ter sido copiado do pipeline ambulatorial. A visualização não reflete as colunas esperadas para internações (ex.: `qtde_internacoes`, `valor_total`).
- **Qualidade de dado/registro**: repetição de valores sugere possível **atribuição no nível errado** (medida no fato vs. agregado) ou **duplicidade** após as junções.


## 2º Resultado

- `df_agg` agrega por `(ano, nome_municipio, faixa_etaria, cid10)` e cria `prop_faixa_etaria = qtde_internacoes / total_ano`.
- `total_ano` é somado **por ano (global)**, não por município. Há também **typo** em município (`SSabará`).

**Conclusões**
- A proporção **não captura a estrutura etária local**; fica diluída no total do ano, misturando municípios.
- A presença de **typos em município** causa fragmentação de categorias, reduzindo poder preditivo.


## 3º Resultado
**O que aparece**
- `prop_60plus` constante (ex.: `0.1`) para diferentes linhas/anos/municípios.
- Cálculo de idosos via `faixa_etaria LIKE "%60%"`.

**Conclusões**
- O filtro **só captura bandas com “60”** e **ignora 70–79 e 80+**, **subestimando** idosos e podendo produzir valores **quase constantes**.
- `prop_60plus` é calculada **por (ano, município)** e depois propagada na junção — coerente —, mas a **definição do conjunto idoso está incorreta**.


## 4º Resultado

**Conclusões**
- **Baixo poder preditivo** no estado atual dos dados/variáveis (R² ~ 0.07–0.09 em RF/GBT).
- **Linear Regression pior que baseline** (R² negativo), indicando **não linearidade** e/ou features pouco informativas para relação com `qtde_internacoes`.
- **Escalonamento (StandardScaler)** é **desnecessário** para RF/GBT e não traz ganho aqui.



## 5º Resultado
**O que aparece**
- `nome_municipio_vec` domina; `prop_60plus` aparece como 0; demais variáveis com importâncias muito baixas.

**Conclusões**
- A leitura de importâncias está **enviesada**:
  - O `featureImportances` retorna importâncias **por coluna expandida** (one-hot). A lista `feature_names` usa apenas os **campos não-expandidos** (ex.: `nome_municipio_vec`), o que **trunca/mapeia erroneamente** as importâncias.
  - Assim, a soma de dezenas/centenas de dummies cai em uma única etiqueta (`nome_municipio_vec`), parecendo dominar tudo.
- O baixo peso de `prop_60plus` é coerente com o **cálculo incorreto** no item 3.



## 🛠️ Próximos Passos

### Dados e Limpeza
- [ ] Corrigir `df.select(...)` para **colunas de internações** (remover campos do ambulatorial).
- [ ] Validar **cardinalidade** nas junções e remover **duplicidades**.
- [ ] Normalizar **nomes de municípios** (corrigir typos, acentos, casing).

### Engenharia de Variáveis
- [ ] Recalcular `prop_faixa_etaria` **por (ano, nome_municipio)** (`total_ano_mun`).
- [ ] Recalcular `prop_60plus` via faixas **60–69/70–79/80+** (ou `60+`) por **(ano, município)**.
- [ ] Considerar **efeitos de calendário** (sazonalidade) e **tendência** (lags: `qtde_internacoes_(t-1)`, médias móveis por município).

### Modelagem e Avaliação
- [ ] Remover `StandardScaler` do caminho de **RF/GBT**; manter para **LR**.
- [ ] Adotar **validação temporal** (ex.: treino ≤ 2016, valida 2017–2018, teste ≥ 2019) com **early stopping**/tuning para GBT.
- [ ] Reportar **RMSE, MAE, MAPE** e analisar **erros por município/faixa** para detectar padrões.


---

## 🔧 Esboço de correções (ideia de código)
```python
# Proporção por município
total_ano_mun = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_internacoes").alias("total_ano_mun"))

df_agg = df_agg.join(total_ano_mun, ["ano", "nome_municipio"]) \
    .withColumn("prop_faixa_etaria_mun", F.col("qtde_internacoes") / F.col("total_ano_mun"))

# Idosos por faixas (não por substring “60”)
faixas_idosas = ["60–69", "70–79", "80+"]
idosos = df_agg.filter(F.col("faixa_etaria").isin(faixas_idosas)) \
    .groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_internacoes").alias("qtde_60plus"))

total = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_internacoes").alias("qtde_total"))

prop_idosos = idosos.join(total, ["ano", "nome_municipio"]) \
    .withColumn("prop_60plus", F.col("qtde_60plus") / F.col("qtde_total"))


