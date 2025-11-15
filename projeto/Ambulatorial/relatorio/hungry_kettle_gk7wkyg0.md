Detalhes da execução

Métrica da execução (3)
mae_test_df
1.3615166936141914
r2_test_df
0.3651639748167451
rmse_test_df
1.9233688363748145

Parâmetros da execução (60)
GBTRegressor.cacheNodeIds
False
GBTRegressor.checkpointInterval
10
GBTRegressor.featuresCol
features
GBTRegressor.featureSubsetStrategy
all
GBTRegressor.impurity
variance
GBTRegressor.labelCol
valor_procedimento_log
GBTRegressor.leafCol
—
GBTRegressor.lossType
squared
GBTRegressor.maxBins
32
GBTRegressor.maxDepth
5
GBTRegressor.maxIter
100
GBTRegressor.maxMemoryInMB
256
GBTRegressor.minInfoGain
0.0
GBTRegressor.minInstancesPerNode
1
GBTRegressor.minWeightFractionPerNode
0.0
GBTRegressor.predictionCol
prediction
GBTRegressor.seed
276210194310129986
GBTRegressor.stepSize
0.1
GBTRegressor.subsamplingRate
1.0
GBTRegressor.validationTol
0.01
OneHotEncoder_1.dropLast
True
OneHotEncoder_1.handleInvalid
error
OneHotEncoder_1.inputCols
['nome_municipio_idx']
OneHotEncoder_1.outputCol
OneHotEncoder_80426919ed99__output
OneHotEncoder_1.outputCols
['nome_municipio_vec']
OneHotEncoder_2.dropLast
True
OneHotEncoder_2.handleInvalid
error
OneHotEncoder_2.inputCols
['faixa_etaria_idx']
OneHotEncoder_2.outputCol
OneHotEncoder_f3c46cb6176a__output
OneHotEncoder_2.outputCols
['faixa_etaria_vec']
OneHotEncoder_3.dropLast
True
OneHotEncoder_3.handleInvalid
error
OneHotEncoder_3.inputCols
['cid10_idx']
OneHotEncoder_3.outputCol
OneHotEncoder_e164f5b85391__output
OneHotEncoder_3.outputCols
['cid10_vec']
OneHotEncoder_4.dropLast
True
OneHotEncoder_4.handleInvalid
error
OneHotEncoder_4.inputCols
['nome_procedimento_idx']
OneHotEncoder_4.outputCol
OneHotEncoder_42d81d8c03fc__output
OneHotEncoder_4.outputCols
['nome_procedimento_vec']
stages
['StringIndexer_1', 'StringIndexer_2', 'StringIndexer_3', 'StringIndexer_4', 'OneHotEncoder_1', 'OneHotEncoder_2', 'OneHotEncoder_3', 'OneHotEncoder_4', 'VectorAssembler', 'GBTRegressor']
StringIndexer_1.handleInvalid
keep
StringIndexer_1.inputCol
nome_municipio
StringIndexer_1.outputCol
nome_municipio_idx
StringIndexer_1.stringOrderType
frequencyDesc
StringIndexer_2.handleInvalid
keep
StringIndexer_2.inputCol
faixa_etaria
StringIndexer_2.outputCol
faixa_etaria_idx
StringIndexer_2.stringOrderType
frequencyDesc
StringIndexer_3.handleInvalid
keep
StringIndexer_3.inputCol
cid10
StringIndexer_3.outputCol
cid10_idx
StringIndexer_3.stringOrderType
frequencyDesc
StringIndexer_4.handleInvalid
keep
StringIndexer_4.inputCol
nome_procedimento
StringIndexer_4.outputCol
nome_procedimento_idx
StringIndexer_4.stringOrderType
frequencyDesc
VectorAssembler.handleInvalid
skip
VectorAssembler.inputCols
['nome_municipio_vec', 'faixa_etaria_vec', 'cid10_vec', 'nome_procedimento_vec', 'idade_media', 'prop_faixa_etaria_mun', 'prop_60plus']
VectorAssembler.outputCol
features

Marca de execução (2)

estimator_class
pyspark.ml.pipeline.Pipeline
estimator_name
Pipeline

Esquema de entrada (7)
prop_faixa_etaria_mun
double
nome_procedimento
string
prop_60plus
double
idade_media
double
nome_municipio
string
faixa_etaria
string
cid10
string

Esquema de saída (0)
Nenhum esquema de saída

Mais propriedades (2)
ID da Execução
836d5f2c-132c-4bf4-8155-792fed8f29e0

ID do Livy
93fac940-6894-4cca-9306-e885680e5e2d


