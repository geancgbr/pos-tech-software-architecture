---
tags: [pos-tech/fase-4, banco-de-dados, revisao]
disciplina: Data Engineering
---

# Revisão - Data Engineering

[[Data Engineering]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Fundamentação
> [!question]- Relacional × não relacional: quais as diferenças?
> Modelo (tabelas com chaves × documentos, chave-valor, colunas, grafos), desempenho (ACID × alta escala em leitura e escrita), esquema (rígido × flexível ou ausente) e escalabilidade (vertical predominante × horizontal). → [[Bancos Relacionais e Não Relacionais]]

> [!question]- O que significa NoSQL, e quando surgiu?
> Not Only SQL: qualquer banco que não siga o modelo relacional. Surgiu no final dos anos 2000, com a queda do custo de armazenamento e a demanda por bases enormes.

> [!question]- Quais os tipos de NoSQL e um exemplo de cada?
> Documentos (MongoDB), colunares (Cassandra), chave-valor (Redis), grafos (Neo4j) e séries temporais (InfluxDB).

> [!question]- O que significa ACID?
> Atomicidade, consistência, isolamento e durabilidade: o que os bancos relacionais são otimizados para garantir.

## Aula 2 - MongoDB
> [!question]- O que é um banco documental?
> Um NoSQL que guarda documentos (geralmente JSON ou XML) com estrutura flexível, útil para dados semiestruturados. → [[DE 02 - Bancos de documentos com MongoDB]]

> [!question]- Como o MongoDB armazena os dados?
> Em documentos BSON (Binary JSON), agrupados em coleções, análogas às tabelas. → [[MongoDB]]

> [!question]- Como o MongoDB garante alta disponibilidade, e para que serve o sharding?
> Com replicação (cópias automáticas em vários servidores, para redundância e tolerância a falhas). O sharding (distribuição em clusters) é "além disso", para desempenho e escalabilidade.

> [!question]- Desde qual versão há transações multi-documento?
> Desde a 4.0.

> [!question]- O MongoDB não tem esquema?
> Tem um "esquema dinâmico": os documentos podem variar, mas é importante pensar num design que atenda à aplicação.

## Aula 3 - Redis
> [!question]- Para que servem os bancos de chave-valor?
> Para acesso muito rápido por chave: cache, sessões, metadados, recomendações. Podem ter limitações em consultas complexas. → [[DE 03 - Bancos de chave-valor com Redis]]

> [!question]- Quais os tipos de dados do Redis?
> Strings, listas, conjuntos, sorted sets e hashes (além de HyperLogLogs, Bitmaps e Streams). → [[Redis]]

> [!question]- Que exemplos de escolha de estrutura o PDF dá?
> Para informações de usuários, pode-se optar por hashes (cada campo, um atributo); para listas de tarefas, a lista pode ser a mais apropriada.

> [!question]- O Redis é grátis? Quais custos existem?
> O software é grátis, mas há custos de hospedagem, de serviços gerenciados (ElastiCache, Azure Cache, Memorystore) e de recursos adicionais.

## Aula 4 - Cassandra
> [!question]- Por que bancos colunares são bons para análise?
> Porque só as colunas relevantes são acessadas, o que acelera agregações e projeções, e têm alta compressão. → [[DE 04 - Bancos colunares com Cassandra]]

> [!question]- Como o Cassandra evita pontos únicos de falha?
> Com uma arquitetura descentralizada em "ring", com particionamento e replicação uniformes entre os nós. → [[Apache Cassandra]]

> [!question]- O que é uma família de colunas?
> A estrutura (também chamada de tabela) que agrupa colunas identificadas pelo nome, sem esquema fixo.

> [!question]- Por que denormalizar no Cassandra?
> Para otimizar as consultas, evitando junções complexas entre tabelas.

## Aula 5 - Neo4j
> [!question]- Quando um banco de grafos é indicado?
> Quando os relacionamentos são tão importantes quanto os dados: redes sociais, recomendações, fraudes. → [[DE 05 - Bancos orientados a grafos com Neo4j]]

> [!question]- Quais os elementos do modelo do Neo4j?
> Nós (entidades), relacionamentos (com tipo, direcionais ou bidirecionais) e propriedades (em nós e relacionamentos). → [[Neo4j]]

> [!question]- Qual a linguagem de consulta do Neo4j?
> A Cypher, declarativa e parecida com a notação de grafos.

## Aula 6 - Cloud e DBaaS
> [!question]- IaaS × PaaS × SaaS?
> IaaS: infraestrutura virtualizada (o usuário controla o SO). PaaS: plataforma completa para desenvolver. SaaS: aplicativo pronto pelo navegador. → [[DBaaS (Database-as-a-Service)]]

> [!question]- O que é DBaaS, e quais os benefícios?
> Um banco gerenciado e configurado pelo provedor de nuvem. Benefícios: implantação fácil, escala automática, alta disponibilidade, manutenção pelo provedor, segurança e menos custo.

> [!question]- Quais os DBaaS da AWS citados?
> RDS, DynamoDB, DocumentDB (compatível com MongoDB), Neptune (grafos) e Aurora (MySQL e PostgreSQL).

## Aula 7 - Microsserviços, ETL e Data Lake
> [!question]- Quais as implicações dos microsserviços nos bancos?
> Banco por serviço, múltiplos tipos de bancos, integração por APIs, desafio de consistência e necessidade de monitoramento centralizado. → [[DE 07 - Bancos de dados e microsserviços]]

> [!question]- O que é ETL?
> Extract, Transform, Load: extrair dados de várias fontes, transformá-los e carregá-los num local centralizado (data warehouse ou data lake). → [[ETL (Extract, Transform, Load)]]

> [!question]- Data Lake × Data Warehouse?
> Data Lake: dados brutos, sem esquema pré-definido, flexível. Data Warehouse: dados estruturados em esquema dimensional ou estrela, otimizado para análise e relatórios. → [[Data Lake e Data Warehouse]]

> [!question]- Quais ferramentas da AWS para ETL, Data Lake e Data Warehouse?
> AWS Glue, Amazon S3 e Amazon Redshift.

## Dúvidas em aberto
- Aula 1: as alternativas surgiram "a partir dos anos 2000" e os NoSQL "no final dos anos 2000"; as aulas 3 a 5 situam a origem de chave-valor, colunares e grafos nos anos 1960 e 1970.
- Aula 4: os colunares teriam surgido nos anos 1970, mas a implementação pioneira citada (Vertica) é dos anos 2000.
- Aula 5: o "O que vem por aí" chama o Neo4j de "uma das principais soluções"; o resumo, de "a principal".
- Aula 5: o PDF chama o Neo4j de "solução comercial", mas lista a Community Edition, gratuita e de código aberto.
- Aula 7: o Data Lake guarda dados "brutos, sem processamento", mas o texto diz que os dados transformados no ETL são carregados nele.

## Pontos fracos (o que errei)
