# 📘 Relatório Final — Modelagem de Machine Learning para Previsão de Internações

## 1. Introdução

Este relatório apresenta a análise completa do processo de modelagem preditiva aplicado à base de **internações hospitalares**, utilizando dados integrados do Lakehouse (F_INTERNACOES + Dimensões Paciente, Município, Tempo e CID).

O objetivo principal da etapa de machine learning foi:

> **Prever a quantidade de internações (qtde_Internacoes)** em função de características demográficas, epidemiológicas e regionais.

Foram aplicados três modelos:

- **GLM Poisson**
- **Random Forest Regressor**
- **Gradient Boosted Trees (GBT)**

Todos os modelos utilizaram:

- Codificação categórica via *StringIndexer + OneHotEncoder*
- Variáveis numéricas derivadas
- Vetorização via *VectorAssembler*
- Split temporal (treino ≤2018, validação 2019–2020, teste ≥2021)

---

## 2. Pré-processamento e Engenharia de Atributos

### 📌 Agregações realizadas

Os dados foram agregados por:

- **ano**
- **nome_municipio**
- **faixa_etaria**
- **cid10**

Gerando:

- `qtde_internacoes`  
- `valor_total`  
- `idade_media`  
- `prop_faixa_etaria_mun`  
- `prop_60plus`  

### 📌 Variáveis utilizadas no modelo

**Numéricas:**
- idade_media  
- valor_total_log (log1p aplicado)  
- prop_faixa_etaria_mun  
- prop_60plus  

**Categóricas:**
- nome_municipio  
- faixa_etaria  
- cid10  

---

## 3. Métricas de Avaliação

A tabela abaixo resume o desempenho dos modelos avaliados:

| Modelo | RMSE | MAE | R² |
|--------|-------------|-------------|-----------|
| **GLM Poisson** | 56.64 | 6.88 | **0.106** |
| **GBT** | 57.16 | 7.10 | **0.089** |
| **Random Forest** | 57.91 | 7.85 | **0.065** |

---

## 4. Análise dos Resultados

### 📌 4.1 Desempenho geral

Nenhum dos modelos apresentou desempenho preditivo alto, o que era esperado, pois:

- Internações são eventos altamente **discretos e irregulares**.
- Fortemente influenciados por fatores externos que **não estão representados** no dataset (ex: surtos, políticas municipais, disponibilidade hospitalar).
- A maior parte dos registros apresenta **valores baixos (0, 1, 2, …)** — dificuldade comum em modelos regressivos.

### 📌 4.2 Interpretação do R²

- O melhor R² foi **0.106** (GLM Poisson).
- Isso significa que **apenas 10,6% da variância total das internações pôde ser explicada** pelo modelo.

Para problemas epidemiológicos reais, isso é comum:  
> Internações não são apenas função de idade + município + CID, mas de condições sociais, climáticas, imunológicas e estruturais.

---

## 5. Análise da Importância das Variáveis

Com base no gráfico fornecido:



Variável Importância

nome_municipio_vec 0.0901
cid10_vec 0.00159
faixa_etaria_vec 0.00059
valor_total_log 0.000006
idade_media 0.0000002
prop_faixa_etaria_mun ≈0
prop_60plus 0




### 📌 Principais conclusões:

### 1️⃣ **A variável mais importante é o MUNICÍPIO**
Assim como na modelagem de atendimentos ambulatoriais, novamente:

> **O município é o principal determinante da quantidade de internações.**

Isso reflete:

- capacidade hospitalar desigual entre municípios,  
- diferenças na estrutura de atendimento,  
- políticas locais,  
- fluxo regional interestadual,  
- oferta de leitos e especialidades.

### 2️⃣ CID10 tem importância muito baixa  
Isso indica que:

- a distribuição das internações por CID é muito semelhante entre faixas etárias e municípios,
- ou que o código CID está **muito granular** para gerar padrões detectáveis pelo modelo.

### 3️⃣ faixa_etaria → baixa importância  
Mesma conclusão:  
Faixa etária sozinha não determina o número total de internações na agregação feita.

### 4️⃣ valor_total_log, idade_media, proporções → irrelevantes  
Isso confirma:

- **Não há relação direta entre valor financeiro total e quantidade de internações.**
- proporções internas (faixa etária/idosos) pouco influenciam o total agregado municipal.

---

## 6. Considerações e Interpretações Avançadas

### ✔ Correlação estrutural forte:

Município é dominante → internar depende mais de **infraestrutura** do que de características do paciente.

### ✔ Modelos não conseguem prever variações irregulares

Internações são eventos extremamente suscetíveis a:

- surtos epidêmicos,
- sazonalidade,
- anos atípicos (ex: COVID),
- mudanças hospitalares,
- contratos de gestão,
- fechamento e abertura de leitos.

Nenhuma dessas variáveis está no dataset.

### ✔ O comportamento discreto da variável-alvo prejudica modelos de regressão

A maioria dos valores são baixos (1,2,3), gerando alto RMSE mesmo com boas previsões relativas.

---

## 7. Recomendações para Melhorar a Modelagem

### 🔧 7.1 Transformar o problema
Ao invés de prever o valor exato (contagem), prever:

- probabilidade de ocorrer internação (binário)
- risco relativo (Poisson ou NegBin com offsets)
- faixas de internação (classificação ordinal)

### 🔧 7.2 Novas features que podem aumentar muito o R²
Adicionar:

- sazonalidade (mês, trimestre)
- clima (temperatura, chuvas)
- indicadores socioeconômicos do município
- oferta hospitalar local (número de leitos SUS)
- taxa de envelhecimento municipal
- grupos de CID (capítulos)
- clusters de municípios

### 🔧 7.3 Reduzir Cardinalidade
Aplicar:

- Target Encoding para município, CID e faixa etária
- Agrupar municípios por perfil
- Criar capítulos do CID

### 🔧 7.4 Testar modelos mais adequados para contagens
- **Poisson Regressor** (com offsets)
- **Negative Binomial Regression**
- **CatBoost** (controle nativo de categóricos)
- **XGBoost com objetivo count:poisson**

---

## 8. Conclusão Geral

### ✔ O aprendizado de máquina aplicado ao problema mostrou:

- Os dados atuais **não possuem variáveis suficientes** para explicar a variabilidade das internações hospitalares.
- O município é disparado o fator mais determinante.
- Outros atributos têm impacto **quase nulo**.
- Modelos de regressão tradicionais (RF/GBT) não são adequados para dados de contagem muito esparsos.
- A modelagem exige informações complementares externas (demográficas, estruturais e sazonais).

### ✔ Ainda assim, a análise é valiosa:

O estudo permitiu identificar padrões estruturais e limitações reais, guiando próximas etapas de modelagem capaz de capturar melhor a lógica epidemiológica das internações.

_Fim do relatório._



