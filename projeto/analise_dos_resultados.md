# 💻📉 Avaliação, Análise e Resultados🩺💊



Este repositório documenta a avaliação dos modelos de **Machine Learning** aplicados, bem como a análise e os resultados obtidos por meio de técnicas de machine learning, aplicadas às bases Ambulatorial, Internações e Mortalidade.



---

## 📊 Organização por Base de Dados


### Ambulatorial
- **Relatório de Avaliação dos Modelos:** [`Ambulatorial/relatorio/`](./Ambulatorial/relatorio/README.md)  
- **Relatório Final — Análise e Resultados:** [`Ambulatorial/analise dos resultados/`](./Ambulatorial/analise_dos_resultados/README.md)  



### Internações
- **Relatório de Avaliação dos Modelos:** [`Internacoes/relatorio/`](./Internacoes/relatorio/README.md)  
- **Relatório Final — Análise e Resultados:** [`Internacoes/analise dos resultados/`](./Internacoes/analise_dos_resultados/README.md)  



### Mortalidade
- **Relatório de Avaliação dos Modelos:** [`Mortalidade/relatorio/`](./Mortalidade/relatorio/README.md)  
- **Relatório Final — Análise e Resultados:** [`Mortalidade/analise dos resultados/`](./Mortalidade/analise_dos_resultados/README.md)  


---

## 📝🔍 Resumo 

### Ambulatorial  
- O modelo GBT apresentou melhor desempenho geral.  
- O município é o principal determinante do valor dos procedimentos.  
- Variáveis clínicas tiveram impacto reduzido.

<img width="1635" height="349" alt="image" src="https://github.com/user-attachments/assets/1588d026-df1d-4620-a3eb-7486c6066239" />


### Internações  
- Os dados atuais **não possuem variáveis suficientes** para explicar a variabilidade das internações hospitalares.
- O município é disparado o fator mais determinante.
- Outros atributos têm impacto **quase nulo**.
- A modelagem exige informações complementares externas (demográficas, estruturais e sazonais).

<img width="1642" height="351" alt="image" src="https://github.com/user-attachments/assets/4fdf7a43-41dd-44fc-b681-6b0e63553513" />


### Mortalidade  
- A mortalidade é fortemente determinada por:
  - idade média da população atendida,  
  - proporção de idosos no conjunto de óbitos,  
  - distribuição de causas (CID-10).  
- O município tem efeito relevante, mas menor que o observado em custos ambulatoriais e internações; aqui o **perfil demográfico/epidemiológico pesa mais** que o fator puramente geográfico.

<img width="1642" height="342" alt="image" src="https://github.com/user-attachments/assets/2ac23033-cd12-4cca-8c22-e698fd52458e" />

---
## 📢⚠️ Conclusão Geral

A aplicação das técnicas de Machine Learning nas bases **Ambulatorial**, **Internações** e **Mortalidade** permitiu identificar padrões relevantes e limitações importantes nos dados disponíveis. Cada base apresentou características específicas que influenciaram diretamente o desempenho dos modelos e a interpretação dos resultados.

No **Ambulatorial**, os modelos apresentaram desempenho satisfatório, com o GBT se destacando como a melhor abordagem. A análise confirmou que o **município** é o principal fator explicativo dos valores dos procedimentos, enquanto as variáveis clínicas mostraram influência reduzida.

Na base de **Internações**, observou-se que a estrutura atual dos dados não contém elementos suficientes para explicar adequadamente a variabilidade das internações hospitalares. Aqui, novamente, o município emerge como o principal determinante, mas a falta de variáveis clínicas, demográficas ou estruturais impede que os modelos alcancem um desempenho robusto. Para avanço significativo, será necessária a **integração de informações complementares**.

Na base de **Mortalidade**, os modelos apresentaram melhor estabilidade e explicabilidade. Diferentemente das demais bases, os resultados indicam que os padrões de mortalidade são influenciados majoritariamente por **aspectos demográficos e epidemiológicos**, como idade, proporção de idosos e distribuição das causas de óbito. O município continua relevante, mas exerce um papel secundário frente às variáveis populacionais.

De forma geral, conclui-se que:

- As bases ambulatoriais e de mortalidade possuem estrutura mais adequada para modelagem preditiva.  
- A base de internações requer **enriquecimento de dados** para permitir modelos mais robustos e interpretáveis.  
- Fatores geográficos são determinantes, mas sua relevância varia conforme o fenômeno analisado.  
- A incorporação de variáveis externas (demográficas, socioeconômicas, assistenciais e sazonais) pode elevar substancialmente a qualidade preditiva dos modelos.

Este repositório sintetiza os achados técnico-analíticos e fornece uma visão clara do comportamento de cada base de dados frente às técnicas de Machine Learning, orientando os próximos passos para evolução da modelagem e para o uso estratégico das informações em saúde.

