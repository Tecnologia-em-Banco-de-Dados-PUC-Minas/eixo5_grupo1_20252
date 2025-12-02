# Relatório de Avaliação dos Modelos de Machine Learning – Mortalidade

## Sumário 📝
- [1. Introdução](#1-introdução)
- [2. Métricas utilizadas](#2-métricas-utilizadas)
- [3. Análise individual dos modelos](#3-análise-individual-dos-modelos)
- [4. Comparação entre modelos válidos](#4-comparação-entre-modelos-válidos)
- [5. Ranking geral](#5-ranking-geral)

---

## 1. Introdução 📢

O objetivo deste relatório é analisar o desempenho de três modelos de Machine Learning aplicados à previsão de indicadores de mortalidade. As execuções incluíram modelos GLM, Random Forest e Gradient Boosted Trees, cujas métricas foram extraídas diretamente do ambiente de experimentação.
Durante a avaliação, observou-se que um dos modelos apresentou métricas extremamente discrepantes — como R² altamente negativo e RMSE muito elevado — caracterizando desempenho inadequado e potencial inconsistência no ajustamento. Por esse motivo, apenas os modelos com resultados estatisticamente plausíveis foram considerados válidos para a comparação final.
Com isso, este relatório oferece uma análise estruturada e segura, permitindo identificar qual modelo apresenta maior capacidade preditiva e melhor estabilidade para uso em aplicações relacionadas à modelagem de mortalidade.


---

## 2. Métricas utilizadas 📊

| Métrica | Interpretação |
|--------|---------------|
| **RMSE** | *Root Mean Squared Error* — erro quadrático médio. Quanto menor, melhor. |
| **R²** | Coeficiente de determinação. Mede a variância explicada. Quanto mais próximo de 1, melhor. Valores muito negativos indicam modelo extremamente inadequado. |


---

## 3. Análise individual dos modelos 👩🏼‍💻👨🏻‍💻

### 3.1 Modelo GLM Poisson

| Métrica | Valor |
|--------|-------|
| **RMSE** | 895.3112 |
| **R²** | -4334.8231 |

### Resumo:
Modelo com **desempenho totalmente inadequado**:
R² extremamente negativo → pior que prever uma constante.
RMSE absurdamente maior que os demais.

➡️ **Modelo considerado inválido/suspeito**.

### Visualização:
<img width="1631" height="354" alt="image" src="https://github.com/user-attachments/assets/9f0b482e-4de8-450d-bd23-b6c525b3d782" />


---

### 3.2 Modelo Random Forest

| Métrica | Valor |
|--------|-------|
| **RMSE** | 5.9447 |
| **R²** | 0.8087 |

### Resumo:
Modelo com boa performance:
R² alto,
RMSE moderado.

Desempenho sólido e consistente.

### Visualização:
<img width="1639" height="359" alt="image" src="https://github.com/user-attachments/assets/a0674bc1-d54b-45b0-9f3b-9ccba6be8915" />


---

### 3.3 Modelo GBT

| Métrica | Valor |
|--------|-------|
| **RMSE** | 3.0851 |
| **R²** | 0.9485 |

### Resumo:
Melhor desempenho entre todos os modelos:
**Menor RMSE**, indicando erro baixo.
**Maior R²**, indicando forte capacidade explicativa.

Modelo altamente competitivo e estável.

### Visualização:
<img width="1635" height="348" alt="image" src="https://github.com/user-attachments/assets/20ff8efe-a4e2-4065-811e-a3f3d203f255" />


---

## 4. Comparação entre modelos válidos 🔍

| Modelo | RMSE ↓ | R² ↑ |
|--------|--------|-------|
| **GBT** | **3.09** | **0.95** |
| **Random Forest** | 5.94 | 0.81 |
| **GLM_Poisson** | 895.31 | -4334.82 |

### Observações:

- **GBT** domina completamente as métricas.
- **Random Forest** vem logo atrás com desempenho sólido.
- **GLM Poisson** é **claramente inválido**, com métricas dilatadas e R² extremamente negativo.

### 4.1 Visualização do desempenho
<img width="1527" height="435" alt="Captura de ecrã 2025-12-02 200937" src="https://github.com/user-attachments/assets/fae1dc40-e290-4b7e-9895-f411a18bc46d" />



---

## 5. Ranking geral 🏆

| Posição | Modelo | Comentário |
|---------|---------|-----------|
| 🥇 1º |  GBT| Melhor RMSE e melhor R². Desempenho claramente superior. |
| 🥈 2º | Random Forest | Bom desempenho geral, mas inferior ao GBT. |
| 🥉 3º |  GLM Poisson | R² extremamente negativo e RMSE muito elevado. Considerado inválido. |

---

