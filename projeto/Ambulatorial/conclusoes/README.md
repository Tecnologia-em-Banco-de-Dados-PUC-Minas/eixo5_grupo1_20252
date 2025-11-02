## Ambulatorial — Conclusões


### 1º Resultado
- **`valor_procedimento = 0`** em procedimentos que deveriam ter valor (ex.: quimioterapia) → indício de **dado faltante/supressão** ou regra de tarifação.
- **Ruído de encoding** (ex.: `RA�PIDO`) → problema de **codificação** nas dimensões.



### 2º Resultado
- `prop_faixa_etaria = qtde_Atendimentos / total_ano`, mas `total_ano` é **global por ano**, não por município.
- Proporções ficam **muito pequenas** e não refletem **estrutura demográfica local**.



### 3º Resultado
- Cálculo de idosos via **`idade_media >= 60`** no nível agregado.
- Pode **subestimar/superestimar** idosos quando há mistura etária nas agregações.


### 4º Resultado
- **Linear Regression com R² ~ 1.0** → **vazamento de alvo**: `valor_procedimento` está nas features.
- RF/GBT com **RMSE muito alto** → alvo com alta amplitude/outliers; métricas contaminadas pelo leakage.



### 5º Resultado
- Domínio de `nome_municipio_vec` e demais variáveis ~0.
- Problemas:
  1) **Leakage** invalida a interpretação.  
  2) **Mapeamento incorreto**: `featureImportances` está no nível **one-hot expandido**, mas os nomes não foram **expandidos/agrupados** por feature original.



## 🛠️ Próximos Passos (sintetizado)

### Correções de Dados (prioridade)
- [ ] Tratar **`valor_procedimento = 0`** (remover/atribuir “desconhecido”/modelar separadamente).
- [ ] **Normalizar encoding** (UTF-8) e corrigir strings corrompidas.
- [ ] **Deduplicar/normalizar** nomes de procedimentos e municípios (trims, casing, acentos).

### Engenharia de Variáveis
- [ ] Recalcular `prop_faixa_etaria` **por (ano, município)**:  
  `total_ano_mun = sum(qtde_Atendimentos) por (ano, município)`  
  `prop_faixa_etaria_mun = qtde_Atendimentos / F.col("total_ano_mun")`
- [ ] Recalcular `prop_60plus` **via faixas** (60–69, 70–79, 80+) **por (ano, município)** (evitar `idade_media`).
- [ ] Considerar **transformação do alvo**: `label = log1p(valor_procedimento)` para reduzir assimetria.

### Modelagem e Avaliação
- [ ] **Remover `valor_procedimento` das features** (é o alvo → leakage).
- [ ] **Separar pipelines**:  
  - LR com `StandardScaler`  
  - RF/GBT **sem** escalonamento
- [ ] **Validação temporal** (ex.: treino ≤ 2021, valida 2022, teste ≥ 2023).
- [ ] Reportar **RMSE, MAE e MAPE** (e reverter `expm1` ao avaliar, se usar log no alvo).
- [ ] Tratar **alta cardinalidade** (top-k categorias + “OUTROS” para `cid10`/`procedimento`/`município`).

---
### 📎 Nota rápida de implementação

```python
# 1) Remover leakage imediatamente
numeric_features = ["idade_media", "prop_faixa_etaria", "prop_60plus", "qtde_Atendimentos"]  # sem 'valor_procedimento'

# 2) Proporções corretas por município (ideia)
total_ano_mun = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_Atendimentos").alias("total_ano_mun"))

df_agg = df_agg.join(total_ano_mun, ["ano", "nome_municipio"]) \
    .withColumn("prop_faixa_etaria_mun", F.col("qtde_Atendimentos") / F.col("total_ano_mun"))

# 3) Idosos por faixa, não por idade média (ideia)
faixas_idosas = ["60–69", "70–79", "80+"]
idosos = df_agg.filter(F.col("faixa_etaria").isin(faixas_idosas)) \
    .groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_Atendimentos").alias("qtde_60plus"))

