# Especificação do Processo de Arquitetura de Dados

## **Introdução**

O presente documento descreve o processo de implementação da arquitetura de dados proposta para o projeto de Ciência de Dados do 5º semestre do curso de Tecnologia em Banco de Dados, ministrado pela PUC Minas. O objetivo é detalhar, de forma técnica, cada etapa envolvida, a fim de garantir clareza no fluxo de informações desde a sua origem até a disponibilização de insights analíticos. A arquitetura foi concebida para assegurar escalabilidade, governança e confiabilidade dos resultados.

## **Fontes de Dados**

As fontes de dados constituem o ponto de partida do projeto. Os dados serão extraídos do site do do SUS. Essas fontes consistem em diversos arquivos externos no formato .dbc, que deverão ser descompactados e, posteriormente, convertidos em CSV. Elas fornecem dados estruturados e não estruturados, os quais serão integrados ao pipeline.

## **Ingestão e Armazenamento de Dados

Os dados coletados são inicialmente armazenados em sua forma bruta em um repositório centralizado e escalável no Microsoft Fabric.
A etapa de ELT (Extract, Load, Transform), realizada por meio da linguagem Python, consistirá na coleta, carregamento e padronização dos dados. Nessa fase, são aplicadas transformações para corrigir inconsistências, remover duplicidades e uniformizar formatos. O resultado é um conjunto de dados tratado e preparado para armazenamento.

## **Análise Exploratória de Dados (EDA)**

A análise exploratória tem como finalidade compreender o perfil dos dados. Serão aplicadas técnicas estatísticas e de visualização para identificar distribuições, correlações e padrões relevantes. Para essa etapa, será utilizada a linguagem de programação Python, com bibliotecas como pandas e matplotlib.

## **Desenvolvimento de Modelos de Machine Learning**

Nesta etapa, serão desenvolvidos modelos preditivos e/ou prescritivos baseados em algoritmos de aprendizado de máquina. O processo contempla a seleção de variáveis, a escolha de algoritmos adequados, o treinamento, a validação e a avaliação de desempenho dos modelos.

## **Visualização dos Dados**

A camada de visualização tem como propósito disponibilizar os resultados das análises e dos modelos em formatos intuitivos e interativos. Serão desenvolvidos dashboards e relatórios no Power BI, de modo a permitir que os stakeholders interpretem as informações de forma ágil e estratégica. Essa camada traduz a complexidade técnica em insights acionáveis para suporte à decisão.

## **Governança de Dados**

A governança de dados assegura conformidade, segurança e confiabilidade em todo o ciclo de vida da informação. Inclui práticas de catalogação, controle de acesso, auditoria, monitoramento e aplicação de políticas de qualidade. Contudo, por se tratar de dados abertos fornecidos pelo SUS, não há necessidade de aplicação de governança de dados, uma vez que já estão públicos e disponíveis para uso.

## **Considerações Finais**
A arquitetura de dados especificada neste documento representa uma abordagem robusta e estruturada para projetos de Ciência de Dados, podendo ser aplicada de forma geral. Ao seguir as etapas descritas, obtém-se uma visão integrada do ciclo de vida da informação, permitindo exploração, modelagem e geração de insights com base em dados consistentes e governados. O cumprimento disciplinado de cada fase garante maior maturidade analítica e suporte efetivo à tomada de decisão.


