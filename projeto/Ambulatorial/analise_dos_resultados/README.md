# 📘 Relatório Final — Análise e Resultados de Machine Learning

## 1. Introdução
Este relatório apresenta a avaliação final dos modelos aplicados na previsão do valor total de procedimentos ambulatoriais, considerando dados do SUS integrados no Lakehouse.

A metodologia aplicada incluiu:
- Pré-processamento e normalização de variáveis
- Junção das tabelas Fato & Dimensões (Paciente, Município, Tempo, CID e Procedimentos)
- Agregações por município, ano, faixa etária, CID e procedimento
- Criação de variáveis derivadas
- Codificação categórica via OneHotEncoder
- Construção de modelos:
  - Gradient Boosted Trees (GBT)
  - Random Forest
  - GLM-Poisson

---

## 2. Métricas Avaliadas
As métricas utilizadas foram:

- **MAE** – Mean Absolute Error  
- **RMSE** – Root Mean Squared Error  
- **R²** – coeficiente de determinação  
- **MAPE** – erro percentual médio  

---

## 3. Resultados Obtidos

### 📊 Gráfico — MAE por Modelo
<img src="data:image/png;base64,{{MAE}}" width="500"/>

### 📊 Gráfico — RMSE por Modelo
<img src="data:image/png;base64,{{RMSE}}" width="500"/>

### 📊 Gráfico — R² por Modelo
<img src="data:image/png;base64,{{R2}}" width="500"/>

### ✔ Tabela consolidada
| Modelo | MAE | RMSE | R² |
|--------|--------|--------|--------|
| **GBT** | 1.36 | 1.92 | 0.36 |
| **Random Forest** | 1.61 | 2.08 | 0.26 |
| **GLM Poisson** | 1.83 | 2.45 | -0.03 |

---

## 4. Importância das Variáveis
### 📊 Gráfico — Importância das Features
<img src="data:image/png;base64,{{FI}}" width="600"/>

---

## 5. Conclusões Gerais
- O modelo GBT apresentou melhor desempenho geral.  
- O município é o principal determinante do valor dos procedimentos.  
- Variáveis clínicas tiveram impacto reduzido.  
- Há espaço para melhorias via engenharia de atributos.

---

## 6. Recomendações
- Reduzir cardinalidade (Target/Frequency Encoding)  
- Agrupar CIDs e procedimentos  
- Testar LightGBM, CatBoost e XGBoost  
- Fazer tuning do GBT  

---

## 7. Encerramento
Modelos e resultados refletem fielmente a complexidade do sistema SUS e oferecem base sólida para análises de políticas públicas.



