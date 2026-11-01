---
tags: [pos-tech/fase-4, banco-de-dados, nosql, conceito]
aliases: [Cassandra, CQL, Cassandra Query Language, Banco colunar, Bancos colunares, Wide Column Store, Column Family Store, Família de colunas]
---

# Apache Cassandra

Banco **distribuído de código aberto**, altamente escalável e disponível, criado pelo **Facebook** e doado à **Apache Software Foundation** ([[DE 04 - Bancos colunares com Cassandra]]).

- **Arquitetura descentralizada** em **"ring"**: dados distribuídos uniformemente, **sem ponto único de falha**.
- **Características**: escalabilidade **linear** · replicação **síncrona e assíncrona** · detecção e **recuperação automática** de falhas · esquema dinâmico · consultas distribuídas em **CQL** (semelhante ao SQL).
- **Modelagem** ("Wide Column Store" / "Column Family Store"): **famílias de colunas** (também chamadas de tabelas) · **chave de partição** decide o nó · **denormalização** para evitar junções · consultas por **chave primária** muito rápidas · projetar o esquema **pelas consultas**.
- **Custos**: grátis (licença **Apache 2.0**), mas em produção provavelmente será preciso hardware, e podem ser necessários recursos adicionais e mão de obra.

**Bancos colunares em geral**: dados de cada coluna juntos; **consultas analíticas** e agregações eficientes, **alta compressão**, colunas flexíveis. Exemplos: Cassandra, HBase, Amazon Redshift; uma das implementações pioneiras: **Vertica** (anos 2000).

Aparece em: [[DE 01 - Fundamentação e SGBDs]], [[DE 04 - Bancos colunares com Cassandra]]
