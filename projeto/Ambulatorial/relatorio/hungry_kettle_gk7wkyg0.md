# 📊 **Relatório da Execução de Machine Learning**
Este relatório consolida as **métricas**, **parâmetros**, **componentes do pipeline**, e **esquemas de entrada**, fornecendo uma visão organizada e comentada da execução do modelo.

---

## 📈 **Métricas da Execução**
As métricas abaixo avaliam o desempenho do modelo no conjunto de teste:

| Métrica | Valor | Explicação |
|--------|--------|------------|
| **MAE (mae_test_df)** | `1.3615` | Erro absoluto médio — indica o erro médio entre valores previstos e reais. |
| **R² (r2_test_df)** | `0.3651` | Coeficiente de determinação — explica quanto da variância o modelo captura. |
| **RMSE (rmse_test_df)** | `1.9233` | Raiz do erro quadrático médio — penaliza mais erros grandes. |

---

## ⚙️ **Parâmetros da Execução**
Abaixo estão os parâmetros utilizados nos componentes, permitindo reprodutibilidade e auditoria.

### 🔥 **GBTRegressor**
O GBTRegressor é um modelo de árvores impulsionadas por gradiente (Gradient Boosted Trees), adequado para problemas de regressão.

| Parâmetro | Valor | Explicação |
|----------|--------|------------|
| cacheNodeIds | False | Define se os nós de árvore serão armazenados em cache. |
| checkpointInterval | 10 | Intervalo entre checkpoints durante o treinamento. |
| featuresCol | features | Nome da coluna de atributos. |
| featureSubsetStrategy | all | Todas as features são usadas em cada divisão. |
| impurity | variance | Critério para medir impureza em regressão. |
| labelCol | valor_procedimento_log | Coluna alvo. |
| lossType | squared | Função de perda quadrática. |
| maxBins | 32 | Nº de divisões para discretização contínua. |
| maxDepth | 5 | Profundidade máxima das árvores. |
| maxIter | 100 | Nº total de iterações (árvores). |
| stepSize | 0.1 | Taxa de aprendizado. |
| subsamplingRate | 1.0 | Proporção de dados usada por iteração. |

---

## 🧩 **OneHotEncoder**
Transforma índices categóricos em vetores esparsos binários (one-hot encoded).

### OneHotEncoder_1 – *nome_municipio*
| Parâmetro | Valor |
|----------|--------|
| dropLast | True |
| handleInvalid | error |
| inputCols | ['nome_municipio_idx'] |
| outputCols | ['nome_municipio_vec'] |

### OneHotEncoder_2 – *faixa_etaria*
| Parâmetro | Valor |
|----------|--------|
| dropLast | True |
| handleInvalid | error |
| inputCols | ['faixa_etaria_idx'] |
| outputCols | ['faixa_etaria_vec'] |

### OneHotEncoder_3 – *cid10*
| Parâmetro | Valor |
|----------|--------|
| dropLast | True |
| handleInvalid | error |
| inputCols | ['cid10_idx'] |
| outputCols | ['cid10_vec'] |

### OneHotEncoder_4 – *nome_procedimento*
| Parâmetro | Valor |
|----------|--------|
| dropLast | True |
| handleInvalid | error |
| inputCols | ['nome_procedimento_idx'] |
| outputCols | ['nome_procedimento_vec'] |

---

## 🔤 **StringIndexer**
Converte colunas categóricas em índices numéricos ordenados por frequência.

### StringIndexer_1 – *nome_municipio*
| Parâmetro | Valor |
|----------|--------|
| handleInvalid | keep |
| inputCol | nome_municipio |
| outputCol | nome_municipio_idx |
| stringOrderType | frequencyDesc |

### StringIndexer_2 – *faixa_etaria*
| Parâmetro | Valor |
|----------|--------|
| handleInvalid | keep |
| inputCol | faixa_etaria |
| outputCol | faixa_etaria_idx |
| stringOrderType | frequencyDesc |

### StringIndexer_3 – *cid10*
| Parâmetro | Valor |
|----------|--------|
| handleInvalid | keep |
| inputCol | cid10 |
| outputCol | cid10_idx |
| stringOrderType | frequencyDesc |

### StringIndexer_4 – *nome_procedimento*
| Parâmetro | Valor |
|----------|--------|
| handleInvalid | keep |
| inputCol | nome_procedimento |
| outputCol | nome_procedimento_idx |
| stringOrderType | frequencyDesc |

---

## 🧱 **VectorAssembler**
Responsável por combinar todas as features em um único vetor usado pelo modelo.

| Parâmetro | Valor |
|----------|--------|
| handleInvalid | skip |
| inputCols | ['nome_municipio_vec', 'faixa_etaria_vec', 'cid10_vec', 'nome_procedimento_vec', 'idade_media', 'prop_faixa_etaria_mun', 'prop_60plus'] |
| outputCol | features |

---

## 🧬 **Pipeline**
O pipeline define a cadeia de transformações aplicada aos dados antes do treinamento do modelo.




