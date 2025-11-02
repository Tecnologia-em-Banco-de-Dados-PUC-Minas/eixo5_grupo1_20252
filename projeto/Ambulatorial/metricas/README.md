# Ambulatorial — Métricas

### 1º Resultado

| ano | faixa_etaria     | idade_media | cid10 | nome_municipio | nome_procedimento         | valor_procedimento |
|-----|------------------|-------------|-------|----------------|---------------------------|--------------------|
| 2021| 80+              | 85.0        | C900  | Belo Horizonte | QUIMIOTERAPIA DE ...      | 0                  |
| 2021| Menor de 1 ano   | 0.0         | M998  | Belo Horizonte | ATENDIMENTO FISIO...      | 635                |
| 2021| 10–19            | 15.0        | C900  | Belo Horizonte | QUIMIOTERAPIA DE ...      | 0                  |
| 2021| 70–79            | 74.0        | M998  | Belo Horizonte | ATENDIMENTO FISIO...      | 635                |
| 2021| 40–49            | 45.0        | C900  | Belo Horizonte | QUIMIOTERAPIA DE ...      | 0                  |

---

### 2º Resultado

| ano | nome_municipio | faixa_etaria | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media        | total_ano | prop_faixa_etaria     |
|-----|----------------|--------------|-------|---------------------------|-------------------|--------------------|--------------------|-----------|-----------------------|
| 2022| Belo Horizonte | 30–39        | 0000  | RADIOGRAFIA DE DE...      | 2550              | 1449398            | 35.0               | 224838270 | 1.134148559317770...  |
| 2022| Belo Horizonte | 10–19        | 0000  | DOSAGEM DE ANTIGE...      | 147221            | 241741808          | 14.127841816045265 | 224838270 | 6.547862158875355E-4  |
| 2022| Belo Horizonte | 40–49        | 0000  | DOSAGEM DE COLINE...      | 142               | 50048              | 45.0               | 224838270 | 6.315650800906803E-7  |
| 2022| Belo Horizonte | 50–59        | 0000  | DOSAGEM DE DESIDR...      | 31382             | 11469456           | 55.0               | 224838270 | 1.395758827000403...  |
| 2022| Belo Horizonte | 20–29        | 0000  | TESTE RA�PIDO TRE...      | 11053             | 1106300            | 25.0               | 224838270 | 4.915978049466401E-5  |

> _only showing top 5 rows_

---

### 3º Resultado

| ano | nome_municipio | faixa_etaria   | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media | total_ano | prop_faixa_etaria     | prop_60plus |
|-----|----------------|----------------|-------|---------------------------|-------------------|--------------------|-------------|-----------|-----------------------|-------------|
| 2021| Belo Horizonte | 01–09          | C833  | QUIMIOTERAPIA DE ...      | 1                 | 0                  | 5.0         | 6431690   | 1.554801304167334E-7  | 0.3         |
| 2021| Belo Horizonte | 60–69          | C343  | QUIMIOTERAPIA DO ...      | 1                 | 110000             | 64.0        | 6431690   | 1.554801304167334E-7  | 0.3         |
| 2021| Belo Horizonte | 80+            | A419  | PARACENTESE DE CA...      | 1                 | 8228               | 85.0        | 6431690   | 1.554801304167334E-7  | 0.3         |
| 2021| Belo Horizonte | 40–49          | C501  | HORMONIOTERAPIA D...      | 17                | 111650             | 45.0        | 6431690   | 2.643162217084468E-6  | 0.3         |
| 2021| Belo Horizonte | Menor de 1 ano | C509  | DETERMINACAO DE R...      | 35                | 646530             | 0.0         | 6431690   | 5.441804564585668E-6  | 0.3         |

> _only showing top 5 rows_

---

### 4º Resultado
| Modelo           | RMSE               | R2                  |
|------------------|--------------------|---------------------|
| LinearRegression | 415.48982622987427 | 0.9999999993356921  |
| RandomForest     | 8155456.598646104  | 0.7440558498191501  |
| GBT              | 7696438.219767242  | 0.7720559704874786  |


---

### 5º Resultado


| Váriavel | Impontância | 
|----------|-------------|
| nome_municipio_vec| 0.1946699277 |
| cid10_vec | 0.0031103803 |
| faixa_etaria_vec | 0.0018939865 |
| valor_procedimento | 1.27435e-05 |
| nome_procedimento_vec | 1.26504e-05|
| prop_60plus | 4.322e-07 |
| idade_media | 3.635e-07 |
| prop_faixa_etaria | 0.0 |
| qtde_Atendimentos| 0.0 |



