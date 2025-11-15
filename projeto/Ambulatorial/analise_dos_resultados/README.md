Relatório Final – Análise e Resultados de
Aprendizado de Máquina
1. Introdução
Este relatório apresenta a avaliação final dos modelos de machine learning utilizados para prever o
valor total de procedimentos ambulatoriais no contexto do SUS. Foram construídos pipelines
completos de preparação dos dados, agregação, engenharia de atributos, codificação categórica e
aplicação de três modelos principais: Gradient Boosted Trees (GBT), Random Forest e
Generalized Linear Model Poisson (GLM).
2. Métricas Avaliadas
As métricas utilizadas para comparação dos modelos foram:
- MAE: Erro Médio Absoluto
- RMSE: Erro Quadrático Médio
- R²: coeficiente de determinação
- MAPE: erro percentual médio
Essas métricas permitem avaliar qualidade preditiva, estabilidade e generalização.
3. Resultados Obtidos
Os modelos válidos apresentaram os seguintes resultados:
- GBT: melhor desempenho geral (MAE ≈ 1.36, RMSE ≈ 1.92, R² ≈ 0.36)
- Random Forest: desempenho intermediário
- GLM Poisson: R² negativo, indicando baixo poder explicativo
O GBT se destacou como o modelo mais consistente e robusto.
4. Importância das Variáveis
A análise de importância das variáveis revelou que o município ('nome_municipio') é o fator mais
determinante para a variação do valor dos procedimentos. Variáveis como faixa etária, idade
média e proporção de idosos apresentaram impacto muito inferior. Isso sugere que fatores
estruturais e administrativos regionais influenciam fortemente os custos no SUS.
5. Conclusões Gerais
• O problema apresenta alta variabilidade e complexidade, dificultando previsões totalmente
precisas.
• O modelo GBT capturou melhor as relações não lineares e as interações entre categorias.
• Modelos lineares não se adequaram ao padrão dos dados.
• A localização geográfica é mais importante do que fatores demográficos.
• Não foram identificados leaks nos modelos finais, mas execuções anteriores sugeriram a
importância de padronizar o pipeline.
6. Recomendações
Para aprimorar os próximos ciclos de modelagem, recomenda-se:
- Reduzir a cardinalidade das variáveis categóricas
- Engenhar novas features (grupos de CID, especialidades, clusters regionais)
- Ajustar hiperparâmetros do GBT
- Considerar técnicas como Target Encoding
- Avaliar novos modelos baseados em boosting e redes neurais
7. Encerramento
Este relatório consolida a análise dos modelos e fornece diretrizes claras para aprimoramentos
futuros. O uso de machine learning demonstrou ser uma abordagem promissora para análise
financeira de procedimentos ambulatoriais.



