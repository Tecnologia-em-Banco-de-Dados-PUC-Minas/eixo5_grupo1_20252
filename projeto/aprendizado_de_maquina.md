# 💻📉 Machine Learning: Dados do SUS 🩺💊


Este repositório documenta exclusivamente o **Machine Learning** aplicado às bases **Ambulatorial**, **Internações** e **Mortalidade**.  
A etapa de **ETL / feature engineering / dados** foi tratada anteriormente; aqui mantemos apenas os **artefatos de ML**:


- **Códigos** → scripts de ML (treino, validação, comparação)
- **Métricas** → resultados (tabelas, gráficos, relatórios)
- **Conclusões** → síntese das descobertas e decisões



No final, você encontrará um **guia rápido dos principais algoritmos de aprendizado de máquina** utilizados, a indicar o que se espera de cada um e os valores a partir dos quais podem ser considerados satisfatórios ou insatisfatórios.

---

## 📚 Sumário — Artefatos de ML

- [Códigos](#sum-codigos)
- [Métricas](#sum-metricas)
- [Conclusões](#sum-conclusoes)

---

Cada base contém **três artefatos**; ao clicar, será direcionado à opção selecionada.


| Base | Códigos | Métricas | Conclusões |
|---|---|---|---|
| **Ambulatorial** |[`Ambulatorial/codigos/`](./Ambulatorial/codigos/) | [`Ambulatorial/metricas/`](./Ambulatorial/metricas/) | [`Ambulatorial/conclusoes/`](./Ambulatorial/conclusoes/) |
| **Internações** |[`Internacoes/codigos/`](./Internacoes/codigos/) | [`Internacoes/metricas/`](./Internacoes/metricas/) | [`Internacoes/conclusoes/`](./Internacoes/conclusoes/) |
| **Mortalidade** |[`Mortalidade/codigos/`](./Mortalidade/codigos/) | [`Mortalidade/metricas/`](./Mortalidade/metricas/) | [`Mortalidade/conclusoes/`](./Mortalidade/conclusoes/) |


---

## 📊 Organização por Base de Dados


**Ambulatorial**  
- **Códigos:** [`Ambulatorial/codigos/`](./Ambulatorial/codigos/)  
- **Métricas:** [`Ambulatorial/metricas/`](./Ambulatorial/metricas/)  
- **Conclusões:** [`Ambulatorial/conclusoes/`](./Ambulatorial/conclusoes/)


**Internações**  
- **Códigos:** [`Internacoes/codigos/`](./Internacoes/codigos/)  
- **Métricas:** [`Internacoes/metricas/`](./Internacoes/metricas/)  
- **Conclusões:** [`Internacoes/conclusoes/`](./Internacoes/conclusoes/)


**Mortalidade**   
- **Códigos:** [`Mortalidade/codigos/`](./Mortalidade/codigos/)  
- **Métricas:** [`Mortalidade/metricas/`](./Mortalidade/metricas/)  
- **Conclusões:** [`Mortalidade/conclusoes/`](./Mortalidade/conclusoes/)



-----

# 💻 Guia Rápido de Modelos de Machine Learning


> **Resumo — modelos, intuito e o que esperar**
Este guia organiza as principais **famílias de modelos de ML** para você escolher rápido o candidato certo e julgar a qualidade sem mistério. A ideia é prática: cada família traz **quando usar**, **métricas ideais** e **regras de bolso** (limiares típicos) para saber se o resultado está **bom** ou **ruim**, sempre a comparar com um **baseline** simples.

**🔍 Famílias e intuito**
- **Classificação**: prever rótulos (sim/não, multi-classes). Útil para crédito, churn, fraude.  
- **Regressão**: prever números contínuos (preço, demanda).  
- **Não supervisionado**: explorar estrutura (clusters) e reduzir dimensão para visualizar/limpar ruído.  
- **Recomendação**: ordenar itens relevantes (top-K) para cada usuário.  
- **Séries temporais**: prever valores ao longo do tempo respeitando sazonalidade/tendência.  
- **Detecção de Anomalia**: achar casos raros/atípicos com mínimo alarme falso.

**🔍 Ao abrir cada seção, você verá:**
- **Quando usar**: em que tipos de dados/problemas o modelo brilha.
- **Métricas certas**: o que medir para não se enganar (ex.: AUPRC em dados desbalanceados).
- **Regras de bolso**: valores de referência (ex.: AUC > 0.75 “bom”) para um primeiro crivo.
- **Sinais de alerta**: dicas rápidas de overfit, underfit ou *tuning* mal feito.
- **Nota de domínio**: lembre-se de ajustar *thresholds* conforme o **custo do erro** (FP vs. FN) no seu caso real.

## 📢Famílias ##


<details>
  <summary><strong>Classificação</strong></summary>

Regressão Logística
- **Uso**: classes binárias; baseline forte e interpretável.  
- **Métricas**: AUC-ROC, AUPRC (desbalanceado), F1, Log-loss, Brier.  
- **Regras de bolso**:  
  - AUC ≈ 0.5 (aleatório) • **> 0.75 bom** • **> 0.85 ótimo**  
  - AUPRC baseline = **prevalência**; **≥ 3×** a prevalência = bom  
  - Brier **< 0.1** = boa calibração

Árvore de Decisão
- **Uso**: interpretável com não linearidades; baseline tabular.  
- **Métricas**: AUC, F1, Accuracy.  
- **Regras**: útil se chega **perto** de RF/GBM com explicações claras.

Random Forest
- **Uso**: tabulares com muitos sinais/outliers.  
- **Métricas**: AUC, F1, Accuracy, OOB score.  
- **Regras**: espere **+2–10 p.p. de AUC** vs. regressão/árvore simples.

Gradient Boosting (XGBoost/LightGBM/CatBoost)
- **Uso**: SOTA em dados tabulares.  
- **Métricas**: AUC, F1, Log-loss.  
- **Regras**: **supera RF** na maioria; se **AUC < RF**, revise tuning/overfit.

SVM (Classificação)
- **Uso**: margens máximas; kernels p/ fronteiras complexas; datasets médios.  
- **Métricas**: AUC, F1.  
- **Regras**: com RBF, **AUC ≥ 0.80** em problemas bem definidos.

k-NN (Classificação)
- **Uso**: baseline não-paramétrico; requer escala.  
- **Métricas**: Accuracy, F1.  
- **Regras**: se **não supera** regressão/árvore, faltam features ou há alto viés.

Naive Bayes
- **Uso**: texto/contagens; muito rápido.  
- **Métricas**: F1, AUC.  
- **Regras**: em bag-of-words, **F1 competitivo**; fora disso, perde para GBM/SVM.

Redes Neurais (MLP, CNN, RNN/Transformers)
- **Uso**: imagem/áudio/texto (CNN/Transformers); tabulares com muito dado (MLP).  
- **Métricas**: Accuracy, F1, AUC (depende).  
- **Regras**:  
  - **Imagem (CNN)**: accuracy **> 90%** comum em datasets limpos  
  - **Texto (Transformers)**: F1 **> 0.85** em intent/NER bem definidos  
  - Em tabulares, só valem se **superarem GBM**

</details>


<details>
  <summary><strong>Regressão</strong></summary>

Linear / Ridge / Lasso
- **Uso**: baseline interpretável.  
- **Métricas**: RMSE, MAE, R², MAPE.  
- **Regras**:  
  - **R² > 0.7** bom • **> 0.9** ótimo (se problema previsível)  
  - **RMSE ≤ 0.8× σ(y)** é bom  
  - **MAPE < 10%** muito bom • **10–20%** razoável

Árvores / Random Forest / GBM (Regressão)
- **Uso**: não linearidades/interações.  
- **Métricas**: RMSE, MAE, R².  
- **Regras**: devem **bater o linear**; se não, falta feature engineering/tuning.

SVR / k-NN (Regressão)
- **Métricas**: MAE, RMSE, R².  
- **Regras**: em datasets menores, esperar **R² ≥ 0.7** quando bem comportado.

</details>


<details>
  <summary><strong>Não Supervisionado</strong></summary>

K-Means
- **Uso**: clusters “esféricos”; padronizar dados.  
- **Métricas**: Silhouette, Calinski-Harabasz, Davies–Bouldin.  
- **Regras**: **Silhouette > 0.5** bom • **> 0.7** ótimo; **DB < 0.5** bom.

DBSCAN
- **Uso**: clusters de forma arbitrária + ruído.  
- **Métricas**: Silhouette; % de ruído.  
- **Regras**: se **ruído > 30–40%**, ajuste `eps/minPts`.

Hierárquico
- **Uso**: dendrogramas; granularidade variável.  
- **Métricas**: Silhouette/CH/DB.  
- **Regras**: buscar “joelhos” claros no dendrograma.

Redução de Dimensão (PCA, t-SNE, UMAP)
- **Uso**: compressão/visualização/ruído.  
- **Métrica (PCA)**: variância explicada.  
- **Regras**: **2–3 PCs > 70%** já ajuda; t-SNE/UMAP avalie separabilidade **visual** (não é métrica global).

</details>


<details>
  <summary><strong>Recomendação</strong></summary>

Colaborativo (MF/ALS) & Conteúdo
- **Métricas**: Precision@K, Recall@K, MAP/NDCG@K, cobertura/diversidade.  
- **Regras**:  
  - **Precision@10 ≥ 0.30** (consumer)  
  - **NDCG@10 ≥ 0.60** indica ranking útil  
  - Compare com baseline “**mais populares**”

</details>


<details>
  <summary><strong>Séries Temporais</strong></summary>

ARIMA / ETS / Prophet
- **Métricas**: MAPE, sMAPE, RMSE (holdout/rolling).  
- **Regras**: **MAPE < 10%** ótimo • **10–20%** aceitável; use **validação temporal**.

GBM/LSTM/Transformers (Time Series)
- **Métricas**: idem acima.  
- **Regras**: **superar Naive/Seasonal Naive**; caso contrário, overfit/tuning.

</details>


<details>
  <summary><strong>Detecção de Anomalias</strong></summary>

Isolation Forest / One-Class SVM / Autoencoders
- **Métricas**: Precision@K, AUROC/AUPRC (se houver rótulos), FPR.  
- **Regras**: **AUPRC ≥ 3–5× prevalência**; manter **FPR < 1–5%** quando custo de FP é alto.

</details>



## 💡 Dicas Práticas

- **Sempre compare com baseline**:  
  - Classificação: AUC baseline = 0.5; **AUPRC baseline = prevalência**  
  - Regressão: compare RMSE/MAE com **σ(y)** e com modelo ingênuo (média/último valor)
- **Validação correta**: k-fold estratificado (i.i.d.) ou **validação temporal** (séries)  
- **Significância**: diferenças **< 1–2 p.p.** podem não ser estatisticamente relevantes  
- **Calibração**: use **Brier** e curvas de calibração quando a probabilidade vira decisão  
- **Custo do erro**: ajuste **threshold** p/ otimizar **precisão/recall** conforme impacto de FP/FN

------

<details>
  <summary><strong>Glossário rápido de métricas</strong></summary>

- **AUC-ROC**: prob. de ranquear positivo acima do negativo (0.5 = aleatório).  
- **AUPRC**: área sob precisão × recall; baseline = prevalência.  
- **F1**: média harmônica entre precisão e recall.  
- **Log-loss**: penaliza probabilidades erradas; menor é melhor.  
- **Brier**: erro quadrático de probabilidade; < 0.1 sugere boa calibração.  
- **Accuracy**: % de acertos; frágil com desbalanceamento.  
- **RMSE/MAE**: erro médio (quadrático/absoluto) na regressão.  
- **R²**: proporção da variância explicada (0–1).  
- **MAPE/sMAPE**: erro percentual (absorve escala).  
- **Silhouette**: coesão × separação de clusters (-1–1).  
- **Calinski-Harabasz / Davies–Bouldin**: índices de qualidade de cluster (maior/melhor e menor/melhor, respectivamente).  
- **Precision@K / Recall@K / NDCG@K**: métricas de ranking/top-K em recomendação.  

</details>



