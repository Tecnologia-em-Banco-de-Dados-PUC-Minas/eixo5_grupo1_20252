# Relatório de Avaliação dos Modelos de Machine Learning- Ambulatorial

## Sumário 📝
- [1. Introdução](#1-introdução)
- [2. Métricas utilizadas](#2-métricas-utilizadas)
- [3. Análise individual dos modelos](#3-análise-individual-dos-modelos)
- [4. Comparação entre modelos válidos](#4-comparação-entre-modelos-válidos)
- [5. Ranking geral](#5-ranking-geral)



---

## 1. Introdução 📢

A análise apresentada neste relatório tem como objetivo avaliar o desempenho de diferentes modelos de Machine Learning aplicados à previsão de valores de procedimentos de saúde. Durante o processo, foram identificados tanto modelos válidos quanto modelos potencialmente problemáticos, os quais exibiram métricas incoerentes — como RMSE extremamente elevado, MAE indefinido ou valores de R² anormalmente altos, que podem indicar data leakage ou falhas no pipeline de preparação dos dados.
Para garantir uma comparação justa e confiável, apenas os modelos com métricas consistentes foram incluídos na avaliação final. Os resultados apresentados aqui visam apoiar a seleção de um modelo robusto, capaz de fornecer previsões precisas e úteis para aplicações operacionais e analíticas na área da saúde.

---

## 2. Métricas utilizadas 📊

| Métrica | Interpretação |
|--------|---------------|
| **MAE** | Erro médio absoluto. Quanto menor, melhor. |
| **RMSE** |Erro quadrático médio. Penaliza mais erros grandes. Quanto menor, melhor. |
| **R²** | Proporção da variância explicada — quanto mais próximo de 1, melhor. |

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

<img width="1640" height="357" alt="image" src="https://github.com/user-attachments/assets/7fa20482-31dd-4c27-ad7a-961e484fed62" />


---

### 3.2 Modelo Random Forest

| Métrica | Valor |
|--------|-------|
| MAE | **1.6059** |
| RMSE | **2.0805** |
| R² | **0.2572** |

### Resumo:
Erro maior e R² mais baixo do que o modelo `GBT`.  
Modelo **mediano**, aceitável, mas não competitivo.

### Visualização:


<img width="1640" height="352" alt="image" src="https://github.com/user-attachments/assets/4e4bb0ce-b71a-4766-a655-bc970da7cc35" />


---

### 3.3 Modelo GLM Poisson

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


<img width="1637" height="346" alt="image" src="https://github.com/user-attachments/assets/eea35627-c488-4711-9fb5-5ddb58507589" />


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
- `Random Forest` é um meio-termo.
- `GLM Poisson` tem desempenho fraco e R² negativo.

  
### 4.1 Visualização do desempenho

<img width="1635" height="349" alt="image" src="https://github.com/user-attachments/assets/32aaac05-08ea-4831-a058-87e4a2bf91cb" />



---

## 5. Ranking geral 🏆


| Posição | Modelo                  | Comentário |
|---------|-------------------------|-----------|
| 🥇 1º   | GBT | Melhor MAE, melhor RMSE e maior R² entre os válidos. |
| 🥈 2º   | Random Forest      | Segundo melhor em todas as métricas. |
| 🥉 3º   | GLM Poisson    | R² negativo e erros maiores. |

---
