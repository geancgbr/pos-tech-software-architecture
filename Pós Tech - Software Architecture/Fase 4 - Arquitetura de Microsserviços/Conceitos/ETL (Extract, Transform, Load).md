---
tags: [pos-tech/fase-4, banco-de-dados, dados, conceito]
aliases: [ETL, Extract, Transform, Load, Extração, Transformação e Carregamento, AWS Glue]
---

# ETL (Extract, Transform, Load)

Processo para **integrar e consolidar** dados de **diferentes fontes**, **transformá-los** num formato adequado e **carregá-los** num local **centralizado**, como um **data warehouse** ou um **data lake** ([[DE 07 - Bancos de dados e microsserviços]]).

| Etapa | O que acontece |
|---|---|
| **Extract** | Dados brutos de bancos transacionais, sistemas legados, CSV |
| **Transform** | Limpeza, filtro, agregação, enriquecimento, harmonização |
| **Load** | Carga num local otimizado para análise, relatórios e **BI** |

- **Por que surgiu**: a **complexidade e diversidade** das fontes e a necessidade de dados consolidados para **análise e decisão**.
- **Nos microsserviços**: cada serviço geralmente tem seu modelo de dados, o que **pode resultar** numa modelagem **fragmentada e inconsistente**. Para minimizar isso, é comum centralizar os dados numa **base única e robusta** (ETL).
- **Ferramentas**: **AWS Glue** (ETL gerenciado, fluxos visuais, catalogação); na GCP, as soluções citadas para ETL são **Google Cloud Storage, BigQuery e Google Cloud Dataflow**. Destinos: ver [[Data Lake e Data Warehouse]].

**Na disciplina Banco de dados em Grafos**: o Neo4j tem conectores para ferramentas de ETL como **Apache Kafka** e **Spark** ([[GR 01 - Fundamentos de grafos e a plataforma Neo4j]]), e a ingestão pode usar plataformas de ETL como **Apache NiFi** e **Apache Airflow** ([[GR 04 - Ingestão de dados]]).

Aparece em: [[DE 07 - Bancos de dados e microsserviços]]
