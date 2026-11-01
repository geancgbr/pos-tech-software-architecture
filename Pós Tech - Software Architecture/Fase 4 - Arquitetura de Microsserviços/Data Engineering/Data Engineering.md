---
tags: [pos-tech/fase-4, banco-de-dados, indice]
disciplina: Data Engineering
fase: 4
aulas: 7
aliases: [Database Engineering, Engenharia de bancos de dados]
---

# Data Engineering

[[Fase 4 - Arquitetura de Microsserviços]] · Revisão → [[Revisão - Data Engineering]]

> [!note] Os nomes dos arquivos dizem "Data engineering"; o texto das aulas chama a disciplina de "engenharia de bancos de dados" e "Database Engineering". Os PDFs não trazem nome de autor.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[DE 01 - Fundamentação e SGBDs]] | [[Bancos Relacionais e Não Relacionais]] |
| 2 | [[DE 02 - Bancos de documentos com MongoDB]] | [[MongoDB]] |
| 3 | [[DE 03 - Bancos de chave-valor com Redis]] | [[Redis]] |
| 4 | [[DE 04 - Bancos colunares com Cassandra]] | [[Apache Cassandra]] |
| 5 | [[DE 05 - Bancos orientados a grafos com Neo4j]] | [[Neo4j]] |
| 6 | [[DE 06 - Cloud e DBaaS]] | [[DBaaS (Database-as-a-Service)]] |
| 7 | [[DE 07 - Bancos de dados e microsserviços]] | [[ETL (Extract, Transform, Load)]], [[Data Lake e Data Warehouse]] |

## Os bancos de cada aula
| Tipo | Banco da aula | Linguagem de consulta | Edições e custos |
|---|---|---|---|
| Documentos | [[MongoDB]] | MQL | Community (grátis), Enterprise, **Atlas** (DBaaS) |
| Chave-valor | [[Redis]] | Linguagem de comando Redis (Redis CLI) | Grátis; ElastiCache, Azure Cache, Memorystore |
| Colunar | [[Apache Cassandra]] | CQL | Grátis (Apache 2.0) |
| Grafos | [[Neo4j]] | Cypher | Community (grátis), Enterprise, **Aura** (DBaaS) |

A tabela é só um mapa de navegação, montado a partir das aulas 2 a 5.

## Ligações com outras disciplinas
- **Desenvolvimento Serverless (Fase 3)**: o [[Amazon DynamoDB]] e o Aurora já tinham aparecido lá.
- **Fase 1**: a nota [[Escalabilidade]] ganhou uma seção desta disciplina, e o Redis aparece em [[Estratégias de Cache]].
- **Clean Architecture (Fase 2)**: a [[Arquitetura Monolítica]] aparece na aula 7, no contraste com os microsserviços.

## Material
PDFs em `~/Desktop/Data Engineering/` ("10SOAT - Fase 4 - Data engineering - Aula 01.pdf" a "Aula 07.pdf").
