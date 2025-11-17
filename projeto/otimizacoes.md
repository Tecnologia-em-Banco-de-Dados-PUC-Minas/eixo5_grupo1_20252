# 🩺 Ajustes Realizados: BASE MORTALIDADE

1. **Modelo Substituído:**  
   Substituído o modelo `LinearRegression` por **GLM Poisson / RF log1**, pois contagem de óbitos é variável discreta e não-negativa; regressão linear é inadequada.  

2. **Ajuste no Select:**  
   - Traz apenas colunas relacionadas à base de mortalidade.  
   - Filtro aplicado ao campo `"MUNICIPIO FORA DE MG"`, que distorcia as estatísticas.  
   - Padronização de nomes de municípios e CIDs inconsistentes.  
   - Remoção de espaços em branco.  

3. **Correção da Proporção de Óbitos:**  
   - Antes: denominador global (por ano).  
   - Agora: cálculo por **ano + município**.  
   - Indicadores pequenos e sem sinal local corrigidos para refletir a **estrutura etária local**.  
   - Coluna renomeada para `prop_faixa_etaria_mun`.  

4. **Ajuste no Critério de Idade:**  
   - Critério `idade_media >= 60` substituído por faixas **60-69**, **70-79** e **80+**.  
   - Valores agora variam conforme município e ano.  
   - Coluna `prop_60plus` ajustada para refletir cálculo real.  

5. **Correção de Target Leakage:**  
   - `qtde_obitos` removido das features.  
   - Proporção global `prop_faixa_etaria` substituída por `prop_faixa_etaria_mun`.  
   - `StandardScaler` removido (não necessário).  
   - Pipeline ajustado para **GLM / RF / GBT**.  

6. **Regressão Corrigida:**  
   - Uso incorreto da regressão linear substituído por **GLM Poisson** (`family="poisson"`, `link="log"`).  
   - Split temporal ajustado.  

7. **Importância das Variáveis:**  
   - Ajuste do bloco final para gerar **importâncias das variáveis** da base.  


---

# 🏥 Ajustes Realizados: BASE INTERNAÇÕES

1. **Limpeza e Padronização:**  
   - Ajuste dos nomes das colunas.  
   - Remoção de colunas desnecessárias.  
   - Correção da nomenclatura do target.  

2. **Correção de Agregações:**  
   - `COUNT` substituído por **SUM**, tornando a variável real e não apenas número de linhas.  
   - Proporção global agora calculada por **município + ano**.  
   - Nova variável: `prop_faixa_etaria_mun`.  

3. **Tratamento de Faixas Etárias:**  
   - Filtro ampliado para englobar demais faixas de idosos.  
   - Tratamento de valores nulos.  

4. **Incorporação do CID10:**  
   - Ajuste do valor total para reduzir **assimetria e outliers**.  

5. **Modelagem:**  
   - Implementação do modelo **GLM Poisson**.  
   - Split temporal ajustado.  
   - Novas métricas adicionadas: **MAE**.  


---

# 🧾 Ajustes Realizados: BASE AMBULATORIAL

1. **Feature Engineering:**  
   - `valor_procedimento` **não usado** como feature (evita superestimação).  
   - Aplicado `log1p` para reduzir impacto de outliers.  
   - Implementação do modelo **GLM Poisson**.  

2. **Limpeza e Padronização:**  
   - Simplificação de imports.  
   - Normalização textual.  
   - Filtro de nulos e correção do target.  

3. **Granularidade dos Dados:**  
   - Agrupamento ajustado de **ano** para **ano + município**, tornando o modelo mais granular e fiel.  

4. **Transformações e Consistência:**  
   - Criação da variável `valor_procedimento_log`.  
   - Consistência nas nomenclaturas para clareza e padrão.  
   - Uso da variável log-transformada para reduzir outliers.  
   - Redução de redundância nas features numéricas para melhorar performance.  

5. **Correções de Leakage e Modelagem:**  
   - Substituído `valor_procedimento` por `valor_procedimento_log`.  
   - Modelo ajustado para **GeneralizedLinearRegression**, adequado para valores positivos.  
   - Split temporal ajustado para evitar **contaminação temporal**.  
   - Métricas implementadas: **MAE** e **MAPE**.  
