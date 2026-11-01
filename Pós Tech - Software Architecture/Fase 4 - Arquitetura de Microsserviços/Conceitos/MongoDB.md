---
tags: [pos-tech/fase-4, banco-de-dados, nosql, conceito]
aliases: [Mongo, MongoDB Atlas, MQL, BSON, Banco de documentos, Bancos documentais]
---

# MongoDB

Banco **de código aberto, orientado a documentos e não relacional**, lançado em **2009**; o nome vem de **"humongous" + "database"** ([[DE 02 - Bancos de documentos com MongoDB]]).

- **Documentos BSON** (Binary JSON), com estrutura **dinâmica** e subdocumentos; guardados em **coleções** (análogas às tabelas).
- **Consultas** em **MQL**, semelhante ao JavaScript (ex.: `db.bills.find({ "due_date": "2023-05-15" })`), com **índices**, consultas ad hoc, geoespaciais e agregações.
- **Alta disponibilidade**: **replicação** (redundância e tolerância a falhas); além disso, **sharding** (distribuição em clusters, para desempenho e escalabilidade). **Transações multi-documento** desde a **4.0**.
- **Modelagem**: incorporar relacionamentos nos documentos em vez de normalizar; há um **"esquema dinâmico"**, que deve ser bem pensado.
- **Edições**: **Community Server** (grátis) · **Enterprise Server** (paga) · **Atlas** (DBaaS em AWS, Azure e Google Cloud).
- Na AWS, o **Amazon DocumentDB** é compatível com MongoDB ([[DE 06 - Cloud e DBaaS]]).

Aparece em: [[DE 01 - Fundamentação e SGBDs]], [[DE 02 - Bancos de documentos com MongoDB]], [[DE 06 - Cloud e DBaaS]]
