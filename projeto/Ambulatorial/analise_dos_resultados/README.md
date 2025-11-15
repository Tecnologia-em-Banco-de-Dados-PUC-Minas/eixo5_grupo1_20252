# Relatório de Avaliação dos Modelos de Machine Learning

## Sumário 📝
- [1. Introdução](#1-introdução)
- [2. Métricas utilizadas](#2-métricas-utilizadas)
- [3. Análise individual dos modelos](#3-análise-individual-dos-modelos)
- [4. Comparação entre modelos válidos](#4-comparação-entre-modelos-válidos)
- [5. Ranking geral](#5-ranking-geral)


---

## 1. Introdução 📢


Durante a análise foram identificados:

- **Modelos válidos**, com métricas consistentes.
- **Modelos inválidos/suspeitos**, com:
  - `MAE = undefined`,
  - `RMSE` na casa de milhões,
  - ou `R²` praticamente igual a 1 (indício de *data leakage* ou erro no pipeline).

Este documento consolida a avaliação de **3 modelos** treinados para previsão de valores de procedimentos.
Somente os modelos válidos foram considerados para o **este relatório**.

---

## 2. Métricas utilizadas 📊

| Métrica | Interpretação |
|--------|---------------|
| **MAE** | *Mean Absolute Error* — erro médio absoluto. Quanto menor, melhor. |
| **RMSE** | *Root Mean Squared Error* — erro quadrático médio. Penaliza mais erros grandes. Quanto menor, melhor. |
| **R²** | Coeficiente de determinação. Mede a proporção da variância explicada pelo modelo. Quanto mais próximo de 1, melhor. |

---

## 3. Análise individual dos modelos 👩🏼‍💻👨🏻‍💻

### 3.1 Modelo GBT

| Métrica | Valor |
|--------|-------|
| MAE | **1.3615** |
| RMSE | **1.9234** |
| R² | **0.3652** |

### Resumo:
Modelo com **melhor combinação de MAE e RMSE** entre os válidos.  
R² é moderado, mas consistente com o problema e sem sinais de erro estrutural.

### Visualização:


<img width="1440" height="368" alt="image" src="https://github.com/user-attachments/assets/531ea392-f61e-4b77-9b13-4fe513b9ce89" />

---

### 3.2 Modelovo Random Forest

| Métrica | Valor |
|--------|-------|
| MAE | **1.6059** |
| RMSE | **2.0805** |
| R² | **0.2572** |

### Resumo:
Erro maior e R² mais baixo do que o modelo `GBT`.  
Modelo **mediano**, aceitável, mas não competitivo.

### Visualização:


<img width="1420" height="360" alt="image" src="https://github.com/user-attachments/assets/2d6a2cc9-1c1c-44ee-8d14-9a8d7b2948fb" />

---

### 3.3 Modelo GLM_Poisson

| Métrica | Valor |
|--------|-------|
| MAE | **1.8304** |
| RMSE | **2.4504** |
| R² | **-0.0304** |

### Resumo:
R² negativo → pior que simplesmente prever a média.  
Modelo com desempenho fraco.
Ainda assim é um modelo válido.

### Visualização:


<img width="1432" height="372" alt="image" src="https://github.com/user-attachments/assets/9a1820da-8993-4f7a-9f53-1f6e59f0bee4" />

---


## 4. Comparação entre os modelos 🔍

Somente os modelos com métricas coerentes foram considerados nesta comparação:

| Modelo                  | MAE ↓ | RMSE ↓ | R² ↑    |
|-------------------------|-------|--------|---------|
| GBT | 1.36 | 1.92 | 0.37 |
| Random Forest      | 1.61  | 2.08   | 0.26    |
| GLM Poisson    | 1.83  | 2.45   | -0.03   |

**Observações:**

- `GBT` domina as três métricas entre os válidos.
- `RandomForest` é um meio-termo.
- `GLM Poisson` tem desempenho fraco e R² negativo.

  
### 4.1 Visualização do desempenho

<img width="1537" height="524" alt="image" src="https://github.com/user-attachments/assets/d410a58e-5997-4960-8229-044f69e95b87" />


---

## 5. Ranking geral 🏆


| Posição | Modelo                  | Comentário |
|---------|-------------------------|-----------|
| 🥇 1º   | GBT | Melhor MAE, melhor RMSE e maior R² entre os válidos. |
| 🥈 2º   | Random Forest      | Segundo melhor em todas as métricas. |
| 🥉 3º   | GLM Poisson    | R² negativo e erros maiores. |

---







