---
tags: [pos-tech/fase-4, banco-de-dados, nosql, aula]
disciplina: Data Engineering
aula: 2
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 02.pdf"
---

# DE 02 - Bancos de documentos com MongoDB

← [[DE 01 - Fundamentação e SGBDs]] · [[Data Engineering]] · Próxima → [[DE 03 - Bancos de chave-valor com Redis]]

> [!summary] Em uma frase
> Os **bancos documentais** armazenam e recuperam informações como **documentos** (geralmente **JSON** ou **XML**), com **estrutura flexível**, úteis para dados **semiestruturados**. O **[[MongoDB]]** (2009) foi pioneiro: documentos **BSON**, **coleções** (análogas às tabelas), consultas em **MQL**, replicação, **sharding** e transações multi-documento desde a 4.0.

## Hands On (vídeo)
As características dos bancos de documentos, a **instalação** do MongoDB e os primeiros passos de configuração. Depois, um **estudo de caso** fictício com operações básicas de manipulação e consulta. Segundo o resumo, foram criadas **coleções** e feitas **inclusão, alteração, exclusão e consulta** de documentos.

## Bancos de dados documentais
- Tipo de banco **não relacional (NoSQL)** que armazena e recupera informações como **documentos**, geralmente em **JSON** (JavaScript Object Notation) ou **XML** (eXtensible Markup Language).
- **Estrutura flexível**: documentos com campos e estruturas diferentes, sem esquema rígido. Especialmente útil com dados **semiestruturados** ou que **variam ao longo do tempo**.
- **Usos**: gerenciamento de conteúdo, sistemas de gerenciamento de documentos, aplicações **web e mobile**, análise de **big data** e personalização de conteúdo.
- **Vantagens**: **escalabilidade horizontal**, **alta disponibilidade** e desempenho.
- **Exemplos**: **MongoDB, Couchbase e DocumentDB**, adotados de startups a grandes corporações.
- **Origem**: a necessidade de lidar com **volumes massivos de dados semiestruturados** (web e mobile, mídias sociais, conteúdo gerado pelo usuário, sensores e **IoT**), em resposta às **limitações dos bancos relacionais** com dados não estruturados e semiestruturados.
- Segundo o "O que vem por aí", os benefícios explorados na aula anterior são **escalabilidade, flexibilidade de esquemas, alto desempenho e baixo custo** (o texto da aula 1 não fala em baixo custo, só na queda do custo de armazenamento).

## O MongoDB
- Banco **de código aberto, orientado a documentos e não relacional**. O nome junta **"humongous"** (enorme) e **"database"**.
- Lançado em **2009**, um dos primeiros e mais conhecidos documentais, **pioneiro** nos documentos flexíveis e na escalabilidade horizontal; o sucesso incentivou o Couchbase e o DocumentDB.
- Dados em **BSON (Binary JSON)**, uma extensão do JSON, com **estrutura dinâmica** e **subdocumentos aninhados**.

| Recurso | O que o PDF diz |
|---|---|
| **Consultas e indexação** | Linguagem de consulta poderosa e **índices**; consultas **ad hoc**, por campos, **geoespaciais** e **agregações** |
| **Alta disponibilidade** | **Replicação** (cópias automáticas em vários servidores) e **sharding** (dados distribuídos em clusters) |
| **Transações** | Desde a **versão 4.0**, **transações multi-documento**, com operações atômicas em vários documentos |
| **Linguagens** | JavaScript, Python, Java, C#, Ruby e muitas outras |
| **Comunidade e suporte** | Comunidade ativa; a empresa oferece serviços comerciais e suporte profissional |

**Exemplo de documento (Código 1)**: uma fatura com `_id: ObjectId(...)`, `customer`, `due_date`, `payment_date`, `amount_paid: 250.75`, `status: "Paid"`, `payment_method`, `invoice_number`, `description`, `notes` e um array `items` com `product`, `quantity` e `unit_price`.

## Custos
| Opção | O que é |
|---|---|
| **Community Server** | Versão **gratuita**, de código aberto, adequada à **maioria dos casos** |
| **MongoDB Enterprise Server** | Edição **paga**: suporte avançado, segurança aprimorada, ferramentas de gerenciamento e monitoramento; preço por número de instâncias e tipo de suporte |
| **MongoDB Atlas** | **DBaaS** na nuvem: clusters em **AWS, Azure e Google Cloud**; preço por configuração e armazenamento |

- Muitas organizações usam a versão **gratuita em produção**; a escolha depende das necessidades do projeto.

## Modelagem e consultas
- Dados em **coleções** (análogas às **tabelas**); cada documento é um registro **independente**, com todos os dados de um objeto ou entidade.
- Consultas em **MQL** (MongoDB Query Language), semelhante à sintaxe do **JavaScript**, baseada em **JSON**, com suporte a índices.
- **Em vez de normalizar** em várias tabelas, é comum **incorporar os relacionamentos** nos documentos.
- **Esquema dinâmico**: documentos podem ter estruturas diferentes, mas isso **não significa que não haja esquema**; é importante pensar num design que atenda à aplicação.

```javascript
db.bills.find({ "due_date": "2023-05-15" })
```

## Referências
Banker, Bakkum e Verch, *MongoDB in Action* · Boaglio · Bradshaw, Brazil e Chodorow, *MongoDB: The Definitive Guide* · Copeland · Merriman e Horowitz · MongoDB Documentation · Paniz · Papiernick · Sadalage e Fowler
