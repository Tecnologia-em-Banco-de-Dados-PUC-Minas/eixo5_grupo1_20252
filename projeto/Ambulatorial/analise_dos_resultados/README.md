# 📘 Relatório Final — Análise e Resultados de Machine Learning- Ambulatorial

## 1. Introdução
Este relatório apresenta a análise dos modelos aplicados à base **Ambulatorial** utilizando dados integrados do Lakehouse (F_AMBULATORIAL + Paciente, Município, Tempo, CID e Procedimentos)

O objetivo principal da etapa de machine learning foi:

> **Prever o valor dos procedimentos ambulatoriais+**

Foram aplicados três modelos:

  - Gradient Boosted Trees (GBT)
  - Random Forest
  - GLM-Poisson


---

## 2. Métricas de Avaliação

A tabela abaixo resume o desempenho dos modelos avaliados:


| Modelo | MAE | RMSE | R² |
|--------|--------|--------|--------|
| **GBT** | 1.36 | 1.92 | 0.36 |
| **Random Forest** | 1.61 | 2.08 | 0.26 |
| **GLM Poisson** | 1.83 | 2.45 | -0.03 |

---

## 3. Análise dos Resultados

### 📌 3.1 Desempenho geral

- Os custos são **altamente heterogêneos** e muito mais sensíveis a:
  - **onde** o procedimento é realizado (município);  
  - características contratuais/estruturais;
do que a:
  - **quem** é o paciente (idade, faixa, perfil CID).
    
 
### 📌 3.2 Principais conclusões


- O modelo conseguiu capturar **padrões importantes**, mas:

  > Ainda há muitos fatores não observados (tipo de prestador, regime de gestão, complexidade tecnológica, pactuações regionais) que não estão nas features.


---

## 4. Conclusões Gerais

### ✔ O aprendizado de máquina aplicado ao problema mostrou:

- O modelo GBT apresentou melhor desempenho geral.  
- O município é o principal determinante do valor dos procedimentos.  
- Variáveis clínicas tiveram impacto reduzido.  

---

## 5. Encerramento
Modelos e resultados refletem fielmente a complexidade do sistema SUS e oferecem base sólida para análises de políticas públicas.



