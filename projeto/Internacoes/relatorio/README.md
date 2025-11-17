# Relatório de Avaliação dos Modelos de Machine Learning- Internações

## Sumário 📝
- [1. Introdução](#1-introdução)
- [2. Métricas utilizadas](#2-métricas-utilizadas)
- [3. Análise individual dos modelos](#3-análise-individual-dos-modelos)
- [4. Comparação entre modelos](#4-comparação-entre-modelos)
- [5. Ranking geral](#5-ranking-geral)

---

## 1. Introdução 📢


Este relatório consolida a avaliação de três modelos de Machine Learning desenvolvidos para prever valores associados a internações hospitalares. A análise considerou diferentes abordagens — incluindo GLM, Random Forest e Gradient Boosted Trees — com foco na qualidade das previsções e na estabilidade das métricas apresentadas.
Modelos que apresentaram resultados inconsistentes, como erros extremamente altos ou métricas indefinidas, foram descartados da comparação principal, a fim de evitar conclusões distorcidas. Assim, o presente documento destaca apenas os modelos cuja performance demonstrou coerência estatística e validade técnica, oferecendo uma visão clara e objetiva sobre seu comportamento preditivo.

---

## 2. Métricas utilizadas 📊

| Métrica | Significado |
|--------|-------------|
| **MAE** | Erro absoluto médio — quanto menor, melhor. |
| **RMSE** | Raiz do erro quadrático médio — penaliza erros altos. Quanto menor, melhor. |
| **R²** | Proporção da variância explicada — quanto mais próximo de 1, melhor. |

---

## 3. Análise individual dos modelos 👩🏻‍💻👨🏽‍💻

---

### 3.1 Modelo **GLM Poisson**

| Métrica | Valor |
|--------|-------|
| **MAE** | 6.8866 |
| **RMSE** | 56.6418 |
| **R²** | 0.1057 |

**Resumo:**  
Desempenho simples, porém consistente. Apesar de possuir o maior RMSE, apresenta o melhor R² entre os modelos.

**Visualização:**  

<img width="1630" height="349" alt="image" src="https://github.com/user-attachments/assets/f8b5dd3d-3219-4ce2-b728-edb9ca313e3d" />



---

### 3.2 Modelo **Random Forest**

| Métrica | Valor |
|--------|-------|
| **MAE** | 7.8531 |
| **RMSE** | 57.9142 |
| **R²** | 0.0651 |

**Resumo:**  
Modelo com o pior desempenho geral: maior MAE, maior RMSE e menor R².

**Visualização:**  

<img width="1644" height="358" alt="image" src="https://github.com/user-attachments/assets/e0693a55-f1de-4e27-b266-45be3c83724e" />



---

### 3.3 Modelo **GBT**

| Métrica | Valor |
|--------|-------|
| **MAE** | 7.1028 |
| **RMSE** | 57.1631 |
| **R²** | 0.0892 |

**Resumo:**  
Apresenta um bom equilíbrio entre as métricas, ficando logo atrás do GLM_Poisson com desempenho sólido.

**Visualização:**  

<img width="1638" height="348" alt="image" src="https://github.com/user-attachments/assets/b3b0cf43-23fb-4053-a7d6-8c85871d5fb9" />



---

## 4. Comparação entre os modelos 🔍

| Modelo | MAE ↓ | RMSE ↓ | R² ↑ |
|--------|-------|--------|-------|
| **GLM Poisson** | **6.89** | **56.64** | **0.106** |
| **GBT** | 7.10 | 57.16 | 0.089 |
| **Random Forest** | 7.85 | 57.91 | 0.065 |

### Observações

- `GLM Poisson` apresenta o melhor MAE, RMSE e R².  
- `GBT` fica muito próximo, com desempenho consistente.  
- `Random Forest` apresenta as piores métricas.

### 4.1 Visualização consolidada  

<img width="1642" height="351" alt="image" src="https://github.com/user-attachments/assets/103cf7c8-b938-4813-914c-8fcac154d8dc" />



---

## 5. Ranking geral 🏆

| Posição | Modelo | Comentário |
|--------|---------|------------|
| 🥇 **1º – GLM Poisson** | Melhor desempenho geral em MAE, RMSE e R². |
| 🥈 **2º – GBT** | Muito próximo do GLM, desempenho robusto. |
| 🥉 **3º – Random Forest** | Modelo mais fraco entre os avaliados. |

---


