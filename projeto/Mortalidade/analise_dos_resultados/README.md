# 📘 Relatório Final — Análise e Resultados de Machine Learning – Mortalidade

## 1. Introdução

Este relatório apresenta a análise dos modelos aplicados à base de **mortalidade**, utilizando dados integrados do Lakehouse (F_MORTALIDADE + dimensões Paciente, Município, Tempo e CID).

O objetivo principal da etapa de machine learning foi:

> **Prever a quantidade de óbitos (QTDE_OBITOS)** em função de características demográficas, epidemiológicas e regionais.

Foram aplicados três modelos:

- GLM Poisson  
- Random Forest Regressor  
- Gradient Boosted Trees (GBT)  

---

## 2. Métricas de Avaliação

A tabela abaixo resume o desempenho dos modelos avaliados no conjunto de teste:

| Modelo         | RMSE     | MAE          | R²           |
|----------------|----------|-------------|--------------|
| **GLM Poisson**| 895.31   | –           | **-4334.82** |
| **Random Forest** | 5.95  | –           | **0.81**     |
| **GBT**        | **3.09** | –           | **0.95**     |

> *Observação:* o código calculou apenas RMSE e R²; o MAE não foi explicitamente avaliado, por isso permanece em branco (“–”).

---

## 3. Análise dos Resultados

### 📌 3.1 Desempenho geral

- O **GLM Poisson** apresentou RMSE extremamente alto e R² **muito negativo**, indicando que o modelo **não conseguiu aprender o padrão dos dados**.
- O **Random Forest** já apresenta bom ajuste, com R² em torno de **0,81**, explicando mais de 80% da variância.
- O **GBT** obteve o **melhor desempenho**, com RMSE próximo de 3 e R² ≈ **0,95**, capturando quase toda a variabilidade da quantidade de óbitos no conjunto de teste.

### 📌 3.2 Principais conclusões

A importância das variáveis no modelo GBT indica que:

- **idade_media** é a variável mais importante → grupos com maior idade média concentram mais óbitos.  
- **prop_60plus** e **prop_faixa_etaria_mun** também são muito relevantes → municípios/combinações com maior proporção de idosos têm mais mortes.  
- **cid10_vec** contribui de maneira relevante, refletindo diferenças entre causas de óbito.  
- **nome_municipio_vec** e **faixa_etaria_vec** têm importância menor, sugerindo que:
  - o **perfil etário e de causa** pesa mais que o simples efeito geográfico do município.



> A mortalidade é principalmente explicada pela **estrutura etária** (idade média, proporção de idosos) e pelo **perfil de causas (CID-10)**, com o município exercendo papel secundário.

---

## 4. Conclusões Gerais

### ✔ O aprendizado de máquina aplicado ao problema mostrou que:

- A mortalidade é fortemente determinada por:
  - idade média da população atendida,  
  - proporção de idosos no conjunto de óbitos,  
  - distribuição de causas (CID-10).  
- O município tem efeito relevante, mas menor que o observado em custos ambulatoriais e internações; aqui o **perfil demográfico/epidemiológico pesa mais** que o fator puramente geográfico.


---

## 5. Encerramento

O estudo de mortalidade mostrou que o uso de machine learning, é capaz de reproduzir com alta fidelidade o padrão histórico de óbitos quando se utiliza a própria estrutura dos dados agregados, destaca o papel central do **envelhecimento populacional** e do **perfil de causas** na explicação da mortalidade,  


