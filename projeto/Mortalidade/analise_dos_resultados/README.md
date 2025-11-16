# 📘 Relatório Final — Modelagem de Machine Learning para Mortalidade

## 1. Objetivo

Modelar a **quantidade de óbitos (QTDE_OBITOS)** agregados por:

- ano  
- município  
- faixa etária  
- CID-10  

usando dados do Lakehouse (F_MORTALIDADE + dimensões Paciente, Região, Tempo e CID), com foco em:

- entender o que explica a variação de óbitos;  
- avaliar a capacidade preditiva dos modelos;  
- interpretar a importância das variáveis.

---

## 2. Preparação dos Dados

### 2.1 Integração e seleção

Foram integradas as tabelas:

- `F_MORTALIDADE`, `D_PACIENTE`, `D_REGIAO`, `D_TEMPO`, `D_CID`

Colunas finais:

- **ano**
- **faixa_etaria**
- **idade_media**
- **cid10**
- **nome_municipio**
- **qtde_Obitos**

Foram removidos registros “FORA DE MG” na dimensão de município.

### 2.2 Agregações

Os dados foram agregados por:

- `ano`, `nome_municipio`, `faixa_etaria`, `cid10`

com as métricas:

- `qtde_Obitos` = soma dos óbitos  
- `idade_media` = média da idade na combinação  

Em seguida foram criadas:

- `total_ano_mun` = total de óbitos por ano + município  
- `prop_faixa_etaria_mun` = qtde_Obitos / total_ano_mun (proporção daquela faixa etária no município e ano)  

### 2.3 Proporção de idosos

Foi calculada:

- `qtde_60plus` = soma dos óbitos nas faixas **60–69, 70–79, 80+**  
- `qtde_total` = total de óbitos por ano + município  

resultando em:

- `prop_60plus` = qtde_60plus / qtde_total  

Essa variável foi depois juntada ao dataset final (`df_ml`).

---

## 3. Features Utilizadas

### 3.1 Variáveis numéricas

- `idade_media`  
- `prop_faixa_etaria_mun`  
- `prop_60plus`  

### 3.2 Variáveis categóricas

- `nome_municipio`  
- `faixa_etaria`  
- `cid10`  

Codificação:

- `StringIndexer` → `*_idx`  
- `OneHotEncoder` → `*_vec`  

Vetor final de features:

- `[nome_municipio_vec, faixa_etaria_vec, cid10_vec, idade_media, prop_faixa_etaria_mun, prop_60plus]`

---

## 4. Modelos Avaliados

Foram ajustados três modelos:

- **GLM Poisson** (`GeneralizedLinearRegression`, família = poisson, link = log)  
- **RandomForestRegressor**  
- **GBTRegressor** (Gradient Boosted Trees)

### 4.1 Split temporal

- **Treino:** `ano <= 2022`  
- **Teste:** `ano > 2022`  

---

## 5. Resultados (RMSE e R²)

| Modelo        | RMSE        | R²          |
|---------------|-------------|-------------|
| GLM_Poisson   | 895.31      | -4334.82    |
| RandomForest  | 5.95        | 0.81        |
| GBT           | **3.09**    | **0.95**    |

### 5.1 Interpretação

- **GLM Poisson**  
  - RMSE extremamente alto e R² muito negativo.  
  - Modelo **inadequado** para esta estrutura de dados; não conseguiu aprender o padrão.

- **Random Forest**  
  - RMSE = 5,95 (baixo na escala da contagem)  
  - R² ≈ 0,81 → explica ~81% da variância dos óbitos.  
  - Modelo forte e coerente.

- **GBT (Gradient Boosted Trees)**  
  - Melhor desempenho geral: RMSE ≈ 3,09 e R² ≈ 0,95.  
  - Explica cerca de **95% da variação da quantidade de óbitos** no conjunto de teste.  
  - Indica um padrão muito bem capturado pelos preditores.

📌 **Conclusão de desempenho:**  
> O **GBT** é o melhor modelo, seguido pelo **Random Forest**, enquanto o **GLM Poisson** falhou na tarefa.

---

## 6. Importância das Variáveis (Modelo GBT)

Tabela de importâncias:

| Variável               | Importância |
|------------------------|------------:|
| `idade_media`          | 0.0244      |
| `prop_60plus`          | 0.0201      |
| `prop_faixa_etaria_mun`| 0.0184      |
| `cid10_vec`            | 0.0161      |
| `nome_municipio_vec`   | 0.0104      |
| `faixa_etaria_vec`     | 0.0094      |

### 6.1 Gráfico de importância (já gerado)
O gráfico mostra:

- `idade_media` no topo, seguida de `prop_60plus` e `prop_faixa_etaria_mun`.
- Variáveis demográficas dominam a explicação.

### 6.2 Interpretação epidemiológica

1. **idade_media – variável mais importante**  
   - Faz todo sentido: quanto maior a idade média do grupo, maior o risco de óbito.  
   - O modelo está capturando claramente o gradiente de risco por idade.

2. **prop_60plus e prop_faixa_etaria_mun – composição etária do município**  
   - Municípios + combinações ano/faixa com maior participação de idosos tendem a apresentar mais óbitos.  
   - Isso traduz o peso do **envelhecimento populacional** na mortalidade.

3. **cid10_vec – perfil de causas de morte**  
   - O código CID-10 contribui de forma relevante.  
   - Certas causas naturalmente possuem maior letalidade, o que o modelo aprendeu.

4. **nome_municipio_vec – menor peso que na Internação/Ambulatorial**  
   - Diferente dos modelos de custo e internações, aqui o município tem importância **secundária**.  
   - Ou seja, **quem você é (perfil etário / causa)** pesa mais do que **onde você mora**, do ponto de vista da contagem de óbitos.

5. **faixa_etaria_vec – redundante com idade_media**  
   - Faz sentido ter importância menor, pois a informação já está em `idade_media` e nas proporções.

---

## 7. Pontos de Atenção e Possível Leakage

O R² de ~0,95 é **muito alto** para um problema real de mortalidade. Isso acende um alerta:

- `prop_60plus` e `prop_faixa_etaria_mun` são calculadas **a partir da própria variável alvo** (`qtde_Obitos`) agregada por ano + município.
- Na prática, isso significa que parte da informação da resposta (alvo) está “voltando” ao modelo como feature.

👉 Isso pode ser visto como uma forma leve de **data leakage** (uso indireto do alvo para construir as features), especialmente se:

- o modelo for aplicado em um cenário em que ainda **não conhecemos** os óbitos daquele ano/município (situação preditiva real).

Ou seja:

> O desempenho excelente (R² ≈ 0,95) deve ser interpretado com cautela, pois algumas features usam a própria informação de óbito agregada.

---

## 8. Comparação com Internações e Atendimentos Ambulatoriais

- **Ambulatorial (custo):**  
  - Variável dominante: **município**  
  - R² moderado  
  - Padrão: custo fortemente ligado à estrutura e contratos locais.

- **Internações:**  
  - Município importante, mas R² baixo (~0,1)  
  - Forte ruído e fatores não observados (surtos, leitos, sazonalidade).

- **Mortalidade:**  
  - Variáveis dominantes: idade média e composição etária (prop_60plus, prop_faixa_etaria_mun)  
  - Município é secundário.  
  - R² muito alto (com risco de leakage).  
  - Padrão: óbitos fortemente determinados pela **estrutura demográfica** + **perfil de causa (CID)**.

---

## 9. Recomendações

### 9.1 Para consolidar o modelo

1. **Reestimar sem usar features derivadas do alvo**
   - Remover ou recalcular `prop_60plus` e `prop_faixa_etaria_mun` usando dados populacionais (censo / projeções), não a própria contagem de óbitos.
   - Isso tornará o modelo mais honesto do ponto de vista preditivo.

2. **Adicionar covariáveis externas**
   - Indicadores socioeconômicos (IDH, renda, escolaridade)
   - Estrutura de saúde (leitos, UTIs, ESF)
   - População residente por faixa etária  
   -> Isso permite modelar risco populacional, não só observação histórica.

3. **Validação mais robusta**
   - Aplicar validação cruzada temporal (ex.: treinar até 2019, testar em 2020; treinar até 2020, testar em 2021 etc.).
   - Verificar se o R² se mantém alto em todos os cortes.

### 9.2 Para uso em política pública

- Utilizar o modelo (sem leakage) como ferramenta de:
  - identificação de **municípios com maior risco de mortalidade em idosos**;  
  - simulação de impacto de envelhecimento populacional sobre óbitos;  
  - priorização de políticas de prevenção, atenção básica e vigilância.

---

## 10. Conclusões Finais

- O modelo GBT para mortalidade apresentou **desempenho muito alto (R² ≈ 0,95)**, mas parte disso pode estar sendo inflada por variáveis derivadas do próprio alvo.
- A análise de importância das variáveis é epidemiologicamente consistente:
  - idade média e proporção de idosos são os principais determinantes;
  - o perfil de causa (CID-10) também é relevante;
  - o município é menos determinante do que a estrutura etária da população, ao contrário do que se observou nos modelos de custo e internações.
- Com ajustes nas features (removendo leakage) e inclusão de dados populacionais e socioeconômicos, este modelo tem grande potencial para apoiar análises de risco de mortalidade e planejamento de saúde pública.

_Fim do relatório._

