---
tags: [pos-tech/fase-4, grafos, neo4j, conceito]
aliases: [LOAD CSV, Neo4j Data Importer, Neo4j Importer, PyIngest, Pyingest]
---

# Ingestão de Dados no Neo4j

As formas de **importar dados** no [[Neo4j]] ([[GR 04 - Ingestão de dados]]).

| Opção | Para quê |
|---|---|
| **`LOAD CSV`** (Cypher) | CSV local, por URL ou em buckets; fluxo linha a linha, com transações e conversões |
| **Neo4j Data Importer** | Interface gráfica, sem código, para CSV e JSON; testes e protótipos (no Workspace do AuraDB ou na versão independente) |
| **PyIngest** | Script Python 3 para grandes volumes (Pandas para CSV, ijson para JSON, blocos configuráveis; `python3 ingest.py <config>`) |
| **Outras** | Scripts em Python, Java, NodeJS; **Spark**; ETL com **Apache NiFi** e **Apache Airflow** |

- **Preparação**: rótulos, relacionamentos e propriedades · **constraints e índices** · as consultas mais importantes.
- **Passos com Cypher**: estrutura do CSV com **IDs únicos** → dados limpos → restrições → carga → índices.
- **PyIngest**: `pre_ingest` → `files` → `post_ingest`; todos os valores são lidos como **strings**; `chunk_size` padrão **1000**.

Aparece em: [[GR 04 - Ingestão de dados]]
