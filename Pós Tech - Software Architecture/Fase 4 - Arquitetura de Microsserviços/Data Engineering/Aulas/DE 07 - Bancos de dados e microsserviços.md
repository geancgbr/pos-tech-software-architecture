---
tags: [pos-tech/fase-4, banco-de-dados, microsservicos, aula]
disciplina: Data Engineering
aula: 7
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 07.pdf"
---

# DE 07 - Bancos de dados e microsserviços

← [[DE 06 - Cloud e DBaaS]] · [[Data Engineering]]

> [!summary] Em uma frase
> Nos **microsserviços**, cada serviço pode ter **seu próprio banco**, o que traz isolamento, mas garantir a **consistência** pode ser um desafio e isso **pode dificultar** o compartilhamento de dados. Para centralizar os dados, usa-se o **[[ETL (Extract, Transform, Load)|ETL]]** (extração, transformação e carregamento) para um **[[Data Lake e Data Warehouse|Data Lake ou Data Warehouse]]**. Na AWS: **Glue, S3 e Redshift**.

## Hands On (vídeos)
**Primeiro vídeo**: a arquitetura de microsserviços e sua influência nas soluções de bancos. **Na sequência**: o **ETL** num ecossistema de dados. Depois, ferramentas de mercado para **ETL, Data Lake e Data Warehouse** e a montagem de uma **arquitetura de banco de dados** numa solução em microsserviços.

## Microsserviços
- Abordagem que **divide uma aplicação** em serviços **menores e independentes**, cada um com uma **funcionalidade específica**, desenvolvido e implantado de forma **autônoma**: **escalabilidade independente** e atualização, testes e deploy sem afetar os demais.
- **Equipes** responsáveis por um ou mais serviços trabalham de forma **independente**; os serviços podem usar **linguagens e tecnologias diferentes**.
- O termo passou a ser usado com mais frequência **a partir de 2011**, quando a **Netflix** adotou a abordagem para seus desafios de escalabilidade (a arquitetura **monolítica** não bastava). Depois vieram **Amazon, Google e Microsoft**, e empresas de alta demanda (e-commerce, financeiro, streaming). Ver [[Arquitetura Monolítica]].

## Implicações nos bancos de dados
| # | Implicação | O que o PDF diz |
|---|---|---|
| 1 | **Banco de dados por serviço** | Cada serviço **pode** ter seu banco: **isolamento e segurança** e modelo de dados próprio |
| 2 | **Múltiplos tipos de bancos** | Ex.: análise de dados com **NoSQL** e gerenciamento de usuários com **relacional** |
| 3 | **Integração** | Os bancos podem ser integrados **por APIs** |
| 4 | **Consistência dos dados** | Pode ser **desafiador**, sobretudo com **atualizações concorrentes**; projetar bem as interfaces |
| 5 | **Monitoramento e gerenciamento** | Ferramentas **centralizadas** para os vários bancos |

- A modelagem é **bastante diferente** da tradicional numa arquitetura **monolítica**.
- **Problemas possíveis**: dificuldade de acesso e compartilhamento entre serviços e equipes, e uma modelagem que **pode resultar** fragmentada e inconsistente em toda a arquitetura.

## ETL (Extract, Transform, Load)
- Para minimizar esses problemas, é comum **centralizar** os dados numa **única base robusta**. Esse processo é o **ETL** (Figura 1).
- **Definição**: integrar e consolidar dados de **diferentes fontes**, transformá-los num formato adequado e carregá-los num local **centralizado** (**data warehouse** ou **data lake**).
- **Origem**: consolidou-se nas últimas décadas, com a necessidade de integrar dados de sistemas operacionais, bancos, planilhas e outros para **análise e decisão**, diante da **complexidade e diversidade das fontes**.

| Etapa | O que acontece |
|---|---|
| **Extração** | Dados brutos de bancos transacionais, **sistemas legados**, arquivos **CSV** etc. |
| **Transformação** | Dados **limpos, filtrados, agregados, enriquecidos e harmonizados** |
| **Carregamento** | Num local centralizado, otimizado para **análise, relatórios e BI** |

- Resultado: análises mais abrangentes, **tendências, padrões** e decisões com base em dados confiáveis.

## Data Lake × Data Warehouse
O destino do ETL (na fase de **carregamento**) precisa comportar a carga e fazer **consultas complexas** com alto desempenho (Figura 2).

| | Data Lake | Data Warehouse |
|---|---|---|
| O que é | Repositório centralizado de dados **brutos**, sem processamento, no **formato original** | Repositório **organizado e estruturado** de dados que passaram por ETL |
| Onde fica | Sistema de arquivos distribuído (**HDFS**) ou nuvem (**Amazon S3**, **Google Cloud Storage**) | — |
| Esquema | **Sem esquema pré-definido**; dados geralmente **não estruturados** | **Normalmente** em esquemas dimensionais ou **em estrela**: **tabelas de fatos** e **de dimensões** |
| Permite / objetivo | Que os dados sejam explorados e transformados de maneiras diferentes | Objetivo principal: ambiente **otimizado para análise e relatórios** |
| Prós e contras | **Mais flexível e escalável**, mas exige **preparação adicional** antes de análises | Consultas complexas e **agregações eficientes** |

> [!note] O PDF diz que o Data Lake guarda dados **brutos, sem processamento**, mas também que, no ETL, os dados **transformados** são carregados no Data Lake, "onde podem ser armazenados em seu formato original".

> [!note] O texto diz que o Data Warehouse "**também** é um repositório organizado e estruturado", o que sugere que o Data Lake também seria, embora os dados dele sejam "geralmente não estruturados".

## ETL na prática (AWS)
| Serviço | Papel |
|---|---|
| **AWS Glue** | **ETL totalmente gerenciado**: fluxos **visuais**, tarefas escaláveis e automatizadas, e **descoberta e catalogação** automática de dados |
| **Amazon S3** | Armazenamento escalável e durável, usado como **Data Lake** (dados brutos, estruturados ou semiestruturados) |
| **Amazon Redshift** | **Data Warehouse** totalmente gerenciado para grandes volumes |

- Na **GCP**: **Google Cloud Storage, BigQuery e Google Cloud Dataflow** (Figura 3).

## Referências
Databricks: ETL · Fowler e Lewis, "Microservices" (2014) · GeeksforGeeks: Data Warehousing · Kimball e Caserta · Kimball e Ross · Newman, *Building Microservices* · Richardson · Oracle: What is ETL?
