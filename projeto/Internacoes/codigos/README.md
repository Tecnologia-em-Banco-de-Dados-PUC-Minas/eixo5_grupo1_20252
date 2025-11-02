# Internações — Códigos (ML)

## 1º Código
```python

# ETAPA 4 - APRENDIZADO DE MÁQUINA

#Foram aplicados 3 modelos de machine learning na base internações são eles:

#LinearRegression → modelo linear simples
#RandomForestRegressor → modelo de floresta aleatória (não linear, robusto)
#GBTRegressor → modelo de Gradient Boosted Trees (ainda mais sofisticado)

from pyspark.sql import SparkSession, functions as F, Window
from pyspark.ml import Pipeline
from pyspark.ml.feature import StringIndexer, OneHotEncoder, VectorAssembler, StandardScaler
from pyspark.ml.regression import LinearRegression, RandomForestRegressor, GBTRegressor
from pyspark.ml.evaluation import RegressionEvaluator
from pyspark.ml.tuning import TrainValidationSplit, ParamGridBuilder

spark = SparkSession.builder.appName("ml_internacoes").getOrCreate()

# Tabelas principais do Lakehouse
F_INTERNACOES = "F_INTERNACOES"
D_PACIENTE = "D_PACIENTE"
D_REGIAO = "D_REGIAO"
D_TEMPO = "D_TEMPO"
D_CID = "D_CID"

# Variável alvo
TARGET = "QTDE_INTERNACOES"

``` 
## 2º Código 
````Python
# Lê tabelas da camada Ouro
f_intern = spark.table(F_INTERNACOES)
d_pac = spark.table(D_PACIENTE)
d_reg = spark.table(D_REGIAO)
d_temp = spark.table(D_TEMPO)
d_cid = spark.table(D_CID)

# Normaliza nomes de colunas
#d_temp = d_temp.withColumnRenamed("ANO", "ano")
#d_pac = d_pac.withColumnRenamed("FAIXA_ETARIA", "faixa_etaria").withColumnRenamed("IDADE_MEDIA", "idade_media")
#d_cid = d_cid.withColumnRenamed("cid10", "cid").withColumnRenamed("cid10", "cid")
#f_intern = f_intern.withColumnRenamed("VALOR_INTERNACOES", "valor_internacoes")

# Junção com dimensões
df = (
    f_intern
    .join(d_pac, f_intern["D_PACIENTE_idD_PACIENTE"] == d_pac["idD_PACIENTE"], "left")
    .join(d_reg, f_intern["D_REGIAO_idD_REGIAO"] == d_reg["idD_REGIAO"], "left")
    .join(d_temp, f_intern["D_TEMPO_idD_TEMPO"] == d_temp["idD_TEMPO"], "left")
    .join(d_cid, f_intern["D_CID_idD_CID"] == d_cid["idD_CID"], "left")
)

df.select("ano", "faixa_etaria", "idade_media", "cid10", "nome_municipio", "valor_internacoes").show(5)


`````
## 3º Código 
````Python

df_agg = (
    df.groupBy("ano", "nome_municipio", "faixa_etaria", "cid10")
      .agg(
          F.count("*").alias("qtde_internacoes"),
          F.sum("valor_internacoes").alias("valor_total"),
          F.avg("idade_media").alias("idade_media")
      )
)

# Proporção de internações por faixa etária (proxy de envelhecimento)
total_ano = df_agg.groupBy("ano").agg(F.sum("qtde_internacoes").alias("total_ano"))
df_agg = df_agg.join(total_ano, "ano").withColumn(
    "prop_faixa_etaria", F.col("qtde_internacoes") / F.col("total_ano")
)

df_agg.show(5)

`````
## 4º Código 
````Python


# Calcula proporção de idosos (faixa_etaria contém "60+")
idosos = df_agg.filter(F.lower(F.col("faixa_etaria")).like("%60%")) \
    .groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_internacoes").alias("qtde_60plus"))

total = df_agg.groupBy("ano", "nome_municipio") \
    .agg(F.sum("qtde_internacoes").alias("qtde_total"))

prop_idosos = idosos.join(total, ["ano", "nome_municipio"]) \
    .withColumn("prop_60plus", F.col("qtde_60plus") / F.col("qtde_total"))

df_ml = df_agg.join(prop_idosos.select("ano", "nome_municipio", "prop_60plus"), ["ano", "nome_municipio"], "left").fillna({"prop_60plus": 0})
df_ml.show(5)
`````
## 5º Código 
````Python

# Define variáveis
numeric_features = ["valor_total", "idade_media", "prop_faixa_etaria", "prop_60plus"]
categorical_features = ["nome_municipio", "faixa_etaria"]

# Codificação
indexers = [StringIndexer(inputCol=c, outputCol=c+"_idx", handleInvalid="keep") for c in categorical_features]
encoders = [OneHotEncoder(inputCols=[c+"_idx"], outputCols=[c+"_vec"]) for c in categorical_features]

# Monta vetor de features
assembler_inputs = [c+"_vec" for c in categorical_features] + numeric_features
assembler = VectorAssembler(inputCols=assembler_inputs, outputCol="features", handleInvalid="skip")
scaler = StandardScaler(inputCol="features", outputCol="scaled_features", withMean=True, withStd=True)


`````
## 6º Código 
````Python


# Modelos
lr = LinearRegression(labelCol="qtde_internacoes", featuresCol="scaled_features")
rf = RandomForestRegressor(labelCol="qtde_internacoes", featuresCol="scaled_features", numTrees=100, maxDepth=8)
gbt = GBTRegressor(labelCol="qtde_internacoes", featuresCol="scaled_features", maxIter=100, maxDepth=5)

# Pipeline comum
stages = indexers + encoders + [assembler, scaler]
pipelines = {
    "LinearRegression": Pipeline(stages=stages + [lr]),
    "RandomForest": Pipeline(stages=stages + [rf]),
    "GBT": Pipeline(stages=stages + [gbt])
}

# Split treino/teste (últimos anos como teste)
train_df = df_ml.filter(F.col("ano") <= 2018)
test_df = df_ml.filter(F.col("ano") > 2018)

evaluator = RegressionEvaluator(labelCol="qtde_internacoes", predictionCol="prediction", metricName="rmse")

results = []
for name, pipeline in pipelines.items():
    model = pipeline.fit(train_df)
    preds = model.transform(test_df)
    rmse = evaluator.evaluate(preds)
    r2 = RegressionEvaluator(labelCol="qtde_internacoes", predictionCol="prediction", metricName="r2").evaluate(preds)
    results.append((name, rmse, r2))

spark.createDataFrame(results, ["Modelo", "RMSE", "R2"]).show()



`````
## 7º Código 
````Python


# Importância das features para o modelo GBT (melhor preditor em geral)
best_model = pipelines["GBT"].fit(train_df)
rf_stage = best_model.stages[-1]
importances = rf_stage.featureImportances.toArray()

feature_names = assembler_inputs
import pandas as pd
fi_df = pd.DataFrame(list(zip(feature_names, importances)), columns=["Variável", "Importância"])
display(fi_df.sort_values(by="Importância", ascending=False))
