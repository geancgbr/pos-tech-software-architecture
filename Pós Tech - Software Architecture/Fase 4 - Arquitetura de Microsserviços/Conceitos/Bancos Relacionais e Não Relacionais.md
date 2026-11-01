---
tags: [pos-tech/fase-4, banco-de-dados, conceito]
aliases: [NoSQL, Not Only SQL, Banco relacional, Bancos relacionais, SGBDR, RDBMS, SGBD, Banco não relacional, ACID]
---

# Bancos Relacionais e Não Relacionais

| | Relacionais (SGBDR / RDBMS) | Não relacionais (NoSQL, "Not Only SQL") |
|---|---|---|
| Origem | No mercado **desde os anos 1970** | Surgiram no **final dos anos 2000**, com a queda do custo de armazenamento |
| Modelo | **Tabelas** (linhas = registros, colunas = atributos), com **chaves primárias e estrangeiras** | **Documentos, chave-valor, colunas, grafos, séries temporais** |
| Desempenho | Otimizados para transações **ACID** (atomicidade, consistência, isolamento, durabilidade) | **Alta escalabilidade** e desempenho em leitura e gravação |
| Esquema | **Rígido e pré-definido** | **Flexível** ou ausente |
| Escalabilidade | A **vertical** foi a predominante | Projetados para a **horizontal** |
| Exemplos | MySQL, Oracle Database, SQL Server, MariaDB, PostgreSQL (a maioria com **SQL**) | Ver a tabela abaixo |

| Tipo de NoSQL | Para quê | Exemplos | Aula |
|---|---|---|---|
| **Documentos** | Dados sem esquema uniforme, em JSON | [[MongoDB]], Couchbase, DocumentDB | [[DE 02 - Bancos de documentos com MongoDB]] |
| **Chave-valor** | Caches, sessões, configuração | [[Redis]], Riak, Amazon DynamoDB | [[DE 03 - Bancos de chave-valor com Redis]] |
| **Colunares** | Consultas analíticas, grandes volumes | [[Apache Cassandra]], HBase, Google Bigtable, Amazon Redshift | [[DE 04 - Bancos colunares com Cassandra]] |
| **Grafos** | Relacionamentos complexos | [[Neo4j]], Amazon Neptune, JanusGraph | [[DE 05 - Bancos orientados a grafos com Neo4j]] |
| **Séries temporais** | Dados que evoluem com o tempo | InfluxDB, TimescaleDB, Prometheus | [[DE 01 - Fundamentação e SGBDs]] |

- Também há bancos **in-memory**, **espaciais** e **de texto completo**.
- Nos microsserviços, cada serviço pode usar **um tipo diferente** de banco ([[DE 07 - Bancos de dados e microsserviços]]).

Aparece em: [[DE 01 - Fundamentação e SGBDs]] a [[DE 07 - Bancos de dados e microsserviços]]
