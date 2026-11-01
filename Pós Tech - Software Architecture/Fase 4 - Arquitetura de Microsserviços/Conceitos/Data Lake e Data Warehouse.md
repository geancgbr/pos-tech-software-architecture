---
tags: [pos-tech/fase-4, banco-de-dados, dados, conceito]
aliases: [Data Lake, Data Warehouse, Esquema estrela, Tabela de fatos, Tabelas de dimensões]
---

# Data Lake e Data Warehouse

Os destinos do [[ETL (Extract, Transform, Load)|ETL]] ([[DE 07 - Bancos de dados e microsserviços]]).

| | Data Lake | Data Warehouse |
|---|---|---|
| Dados | **Brutos**, no formato original, geralmente **não estruturados** | **Pré-processados, limpos e transformados** |
| Esquema | **Sem esquema pré-definido** | **Normalmente** dimensional ou **em estrela** (tabelas de **fatos** e de **dimensões**) |
| Onde | **HDFS**, **Amazon S3**, **Google Cloud Storage** | **Amazon Redshift** (o BigQuery é citado entre as soluções da GCP para ETL) |
| Pontos fortes | **Flexível e escalável** | Consultas complexas e **agregações eficientes** para relatórios |
| Observação | Exige **preparação adicional** antes das análises | Abordagem **mais estruturada** (dados pré-processados antes da carga) |

> [!note] O PDF diz que o Data Lake guarda dados brutos, sem processamento, mas também que os dados transformados no ETL são carregados nele, "em seu formato original".

Aparece em: [[DE 07 - Bancos de dados e microsserviços]]
