# Mortalidade — Métricas

### 1º Resultado

| ano | faixa_etaria     | idade_media | cid10 | nome_municipio | nome_procedimento         | valor_procedimento |
|-----|------------------|-------------|-------|----------------|---------------------------|--------------------|
|2022 |             30–39|         35.0|   I219|MUNICÍPIO FORA DE MG|          1|
|2022 |             20–29|         25.0|   I219|MUNICÍPIO FORA DE MG|          1|
|2022 |               80+|         85.0|   I219|MUNICÍPIO FORA DE MG|          1|
|2022 |             40–49|         45.0|   I219|MUNICÍPIO FORA DE MG|          1|
|2022 |             60–69|         65.0|   I219|MUNICÍPIO FORA DE MG|          1|

> _only showing top 5 rows_


---

### 2º Resultado

| ano | nome_municipio | faixa_etaria | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media        | total_ano | prop_faixa_etaria     |
|-----|----------------|--------------|-------|---------------------------|-------------------|--------------------|--------------------|-----------|-----------------------|
|2022|      Almenara|         20–29| E149|         12|       25.0|  1600041|7.499807817424678E-6|
|2022|         Araxá|         70–79| X999|          4|       74.0|  1600041|2.499935939141559...|
|2022|Belo Horizonte|         40–49| I249|          2|       45.0|  1600041|1.249967969570779...|
|2022|Belo Horizonte|Menor de 1 ano| C259|        253|        0.0|  1600041|1.581209481507036...|
|2022|Belo Horizonte|         50–59| I219|        676|       55.0|  1600041|4.224891737149235...|


> _only showing top 5 rows_

---

### 3º Resultado

| ano | nome_municipio | faixa_etaria   | cid10 | nome_procedimento        | qtde_Atendimentos | valor_procedimento | idade_media | total_ano | prop_faixa_etaria     | prop_60plus |
|-----|----------------|----------------|-------|---------------------------|-------------------|--------------------|-------------|-----------|-----------------------|-------------|
|2022|      Almenara|         20–29| E149|         12|       25.0|  1600041|7.499807817424678E-6|0.29978838466964497|
|2022|         Araxá|         70–79| X999|          4|       74.0|  1600041|2.499935939141559...|0.29969556883526893|
|2022|Belo Horizonte|         40–49| I249|          2|       45.0|  1600041|1.249967969570779...|0.29965878625396053|
|2022|Belo Horizonte|Menor de 1 ano| C259|        253|        0.0|  1600041|1.581209481507036...|0.29965878625396053|
|2022|Belo Horizonte|         50–59| I219|        676|       55.0|  1600041|4.224891737149235...|0.29965878625396053|


> _only showing top 5 rows_

---

### 4º Resultado
| Modelo           | RMSE               | R2                  |
|------------------|--------------------|---------------------|
|LinearRegression  |0.20637454266599922 |0.9997674140371855   |
|    RandomForest  |  8.046786795759118 |  0.64639675502611   |
|             GBT  |   6.24856462006486 |0.7867781124730892   |



---

### 5º Resultado


| Váriavel | Impontância | 
|----------|-------------|
|LinearRegression|0.20637454266599922|0.9997674140371855|
|    RandomForest|  8.046786795759118|  0.64639675502611|
|             GBT|   6.24856462006486|0.7867781124730892|
