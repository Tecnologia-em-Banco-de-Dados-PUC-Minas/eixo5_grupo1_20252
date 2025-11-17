# 📘 Relatório Final — Análise e Resultados de Machine Learning- Internações

## 1. Introdução

Este relatório apresenta a análise dos modelos aplicado à base de **internações hospitalares**, utilizando dados integrados do Lakehouse (F_INTERNACOES + Dimensões Paciente, Município, Tempo e CID).

O objetivo principal da etapa de machine learning foi:

> **Prever a quantidade de internações** em função de características demográficas, epidemiológicas e regionais.

Foram aplicados três modelos:

- GLM Poisson
- Random Forest Regressor
- Gradient Boosted Trees (GBT)



## 2. Métricas de Avaliação

A tabela abaixo resume o desempenho dos modelos avaliados:

| Modelo | RMSE | MAE | R² |
|--------|-------------|-------------|-----------|
| **GLM Poisson** | 56.64 | 6.88 | **0.106** |
| **GBT** | 57.16 | 7.10 | **0.089** |
| **Random Forest** | 57.91 | 7.85 | **0.065** |

---

## 3. Análise dos Resultados

### 📌 3.1 Desempenho geral

Nenhum dos modelos apresentou desempenho preditivo alto, o que era esperado, pois:

- Internações são eventos altamente **discretos e irregulares**.
- Fortemente influenciados por fatores externos que **não estão representados** no dataset (ex: surtos, políticas municipais, disponibilidade hospitalar).


### 📌 3.2 Principais conclusões


> **O município é o principal determinante da quantidade de internações.**

Isso reflete:

- capacidade hospitalar desigual entre municípios,  
- diferenças na estrutura de atendimento,  
- políticas locais,  
- fluxo regional interestadual,  
- oferta de leitos e especialidades.

---

## 4. Conclusões Gerais

### ✔ O aprendizado de máquina aplicado ao problema mostrou:

- Os dados atuais **não possuem variáveis suficientes** para explicar a variabilidade das internações hospitalares.
- O município é disparado o fator mais determinante.
- Outros atributos têm impacto **quase nulo**.
- A modelagem exige informações complementares externas (demográficas, estruturais e sazonais).

---

## 5. Encerramento
O estudo permitiu identificar padrões estruturais e limitações reais, guiando próximas etapas de modelagem capaz de capturar melhor a lógica epidemiológica das internações.





