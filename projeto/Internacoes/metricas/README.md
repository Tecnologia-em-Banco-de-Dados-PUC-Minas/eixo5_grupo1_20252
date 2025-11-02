# Internações — Métricas

### 1º Resultado

| ano | faixa_etaria     | idade_media | cid10 | nome_municipio | nome_procedimento         | valor_procedimento |
|-----|------------------|-------------|-------|----------------|---------------------------|--------------------|
| 2008|             70–79|         74.0|   F205|       Barbacena|                     131348|
| 2008|             20–29|         25.0|   F205|       Barbacena|                     131348|
| 2008|             30–39|         35.0|   F205|       Barbacena|                     131348|
| 2008|             40–49|         45.0|   F205|       Barbacena|                     131348|
| 2008|    Menor de 1 ano|          0.0|   F205|       Barbacena|                     131348|
  
> _only showing top 5 rows_


---

### 2º Resultado


| ano | nome_municipio | faixa_etaria | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media        | total_ano | prop_faixa_etaria     |
|-----|----------------|--------------|-------|---------------------------|-------------------|--------------------|--------------------|-----------|-----------------------|
|2012|  Juiz de Fora|         10–19| I738|              19|    5181700|       16.0|      480| 0.03958333333333333|
|2015|       SSabará|           80+| G328|              23|    4935639|       85.0|      650| 0.03538461538461538|
|2015|     Barbacena|         50–59| F205|              12|    1491436|       55.0|      650|0.018461538461538463|
|2018|  Juiz de Fora|         01–09|  F03|               8|    1334529|        5.0|     2560|            0.003125|
|2020|  Juiz de Fora|Menor de 1 ano| I694|              38|    8207550|        0.0|     2480| 0.01532258064516129|

> _only showing top 5 rows_

---

### 3º Resultado

| ano | nome_municipio | faixa_etaria   | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media | total_ano | prop_faixa_etaria     | prop_60plus |
|-----|----------------|----------------|-------|---------------------------|-------------------|--------------------|-------------|-----------|-----------------------|-------------|
|2012|  Juiz de Fora|         10–19| I738|              19|    5181700|       16.0|      480| 0.03958333333333333|        0.1|
|2015|       SSabará|           80+| G328|              23|    4935639|       85.0|      650| 0.03538461538461538|        0.1|
|2015|     Barbacena|         50–59| F205|              12|    1491436|       55.0|      650|0.018461538461538463|        0.1|
|2018|  Juiz de Fora|         01–09|  F03|               8|    1334529|        5.0|     2560|            0.003125|        0.1|
|2020|  Juiz de Fora|Menor de 1 ano| I694|              38|    8207550|        0.0|     2480| 0.01532258064516129|        0.1|

> _only showing top 5 rows_

---

### 4º Resultado

| Modelo           | RMSE               | R2                  |
|------------------|--------------------|---------------------|
|LinearRegression  |74.25057591843085  |-0.5368275261298188|
|    RandomForest  |57.72480202578457  |0.07113974193255235|
|             GBT  |57.10335164262287  |0.09103182753026051|


---

### 5º Resultado


| Váriavel | Impontância | 
|----------|-------------|
| nome_municipio_vec | 0.0894773097 |
| faixa_etaria_vec | 0.0130719367 |
| valor_total | 0.001896231 |
| prop_faixa_etaria | 0.0001199036 |
| idade_media | 1.0445e-06 |
| prop_60plus | 0.0 |
