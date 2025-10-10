## **Pré-Processamento de Dados**

Na terceira fase do projeto, os dados já foram reunidos e encontram-se disponíveis, provenientes de diversas fontes e em múltiplos formatos. Nesta etapa, o foco principal é realizar o pré-processamento, assegurando que as informações estejam organizadas, padronizadas e adequadas para as próximas análises e para o treinamento de modelos de machine learning. Essa etapa é essencial para garantir a qualidade e a uniformidade dos dados, influenciando diretamente a precisão e a confiabilidade dos resultados obtidos.

### **Análise Exploratória**

**Camada Bronze**

Para a análise dos dados, optamos por utilizar o modelo de arquitetura em medalhão, que organiza as informações em camadas progressivas de qualidade e refinamento. Durante essa etapa, identificamos que os arquivos no formato .csv estavam segmentados por mês. Assim, na camada bronze, centralizamos e armazenamos esses conjuntos de dados brutos em três repositórios do **SharePoint**, garantindo uma melhor estruturação e facilidade de gerenciamento das informações. 

<p align="center">
  <img src="arquivos/pre_processamento.png" alt="Sharepoint" width="600"/>
</p>

**Camada Silver**

Para o tratamento inicial dos dados, optamos por utilizar a ferramenta **Dataflow Gen2**, disponível no Fabric, com o objetivo de simplificar e agilizar o processo de transformação por meio do **Power Query**. Durante essa etapa, enfrentamos alguns desafios, já que trabalhamos com três bases de dados distintas, o que exigiu a padronização dos formatos dos campos existentes.

Padronizamos a coluna Sexo para os valores “F” e “M”, e realizamos um mapeamento *DE/PARA* na coluna *Raça Cor* , alinhando-a ao padrão estabelecido pelo *Instituto Brasileiro de Geografia e Estatística (IBGE)*. As colunas de Data foram convertidas para o tipo **DATE**, no formato *dd/MM/yyyy*, enquanto os demais campos foram ajustados para seus tipos de dados adequados.

Após a padronização, passamos para a etapa de limpeza, removendo colunas que não seriam utilizadas nas análises e excluindo linhas com valores nulos, garantindo assim uma base mais consistente e confiável para a próxima etapa. 

**Camada Ouro**

