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

- **Ambulatorial:**  
- O modelo GBT apresentou melhor desempenho geral.  
- O município é o principal determinante do valor dos procedimentos.  
- Variáveis clínicas tiveram impacto reduzido.

- **Internações:**  
  - Município importante, mas R² baixo (~0,1)  
  - Forte ruído e fatores não observados (surtos, leitos, sazonalidade).

- **Mortalidade:**  
  - Variáveis dominantes: idade média e composição etária (prop_60plus, prop_faixa_etaria_mun)  
  - Município é secundário.  
  - Padrão: óbitos fortemente determinados pela **estrutura demográfica** + **perfil de causa (CID)**.
