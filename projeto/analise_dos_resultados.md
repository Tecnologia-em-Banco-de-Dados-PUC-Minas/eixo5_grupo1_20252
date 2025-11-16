# 💻📉 Avaliação, Análise e Resultados🩺💊



Este repositório documenta a avaliação dos modelos aplicados, bem como a análise e os resultados obtidos por meio de técnicas de machine learning, aplicadas às bases Ambulatorial, Internações e Mortalidade.



---

## 📊 Organização por Base de Dados


**Ambulatorial**
- **Relatório de Avaliação dos Modelos de Machine Learning:** [`Ambulatorial/relatorio/`](./Ambulatorial/relatorio/README.md)  
- **Relatório Final — Análise e Resultados de Machine Learning:** [`Ambulatorial/analise dos resultados/`](./Ambulatorial/analise_dos_resultados/README.md)  



**Internações**
- **Relatório de Avaliação dos Modelos de Machine Learning:** [`Internacoes/relatorio/`](./Internacoes/relatorio/README.md)  
- **Relatório Final — Análise e Resultados de Machine Learning:** [`Internacoes/analise dos resultados/`](./Internacoes/analise_dos_resultados/README.md)  



**Mortalidade**
- **RRelatório de Avaliação dos Modelos de Machine Learning:** [`Internacoes/relatorio/`](./Internacoes/relatorio/README.md)  
- **Relatório Final — Análise e Resultados de Machine Learning:** [`Mortalidade/analise dos resultados/`](./Mortalidade/analise_dos_resultados/README.md)  




# 📝🔍 Resumo 

## Ambulatorial  
- O modelo GBT apresentou melhor desempenho geral.  
- O município é o principal determinante do valor dos procedimentos.  
- Variáveis clínicas tiveram impacto reduzido.  


## Internações  
- Os dados atuais **não possuem variáveis suficientes** para explicar a variabilidade das internações hospitalares.
- O município é disparado o fator mais determinante.
- Outros atributos têm impacto **quase nulo**.
- A modelagem exige informações complementares externas (demográficas, estruturais e sazonais).

## Mortalidade  
- A mortalidade é fortemente determinada por:
  - idade média da população atendida,  
  - proporção de idosos no conjunto de óbitos,  
  - distribuição de causas (CID-10).  
- O município tem efeito relevante, mas menor que o observado em custos ambulatoriais e internações; aqui o **perfil demográfico/epidemiológico pesa mais** que o fator puramente geográfico.
