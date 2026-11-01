---
tags: [pos-tech/fase-4, microsservicos, saga, indice]
disciplina: SAGA Pattern
fase: 4
aulas: 5
---

# SAGA Pattern

[[Fase 4 - Arquitetura de Microsserviços]] · Revisão → [[Revisão - SAGA Pattern]] · Conceito → [[Saga]]

> [!note] Os PDFs não trazem nome de autor. As aulas 1 a 3 são teóricas (origem, coreografia × orquestração, falta de isolamento); as aulas 4 e 5 usam um projeto de referência da FIAP Store com três serviços (pedido, cobrança e entrega).

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[SAGA 01 - Introdução ao padrão SAGA]] | [[Saga]], [[ACID]], [[Transações Compensatórias]], [[XA (Extended Architecture)]] |
| 2 | [[SAGA 02 - Orquestração e coreografia]] | Coreografia × orquestração ([[Saga]]), AWS Step Functions, Google Cloud Workflows |
| 3 | [[SAGA 03 - Lidando com a falta do I do ACID]] | [[Anomalias de Dados em Sagas]] (Lost Updates, Dirty Reads, Pessimistic View, Reread Value), [[Níveis de Isolamento de Transações]] |
| 4 | [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]] | Projeto de referência, [[Arquitetura Hexagonal]], H2, Swagger, [[RabbitMQ]], [[Apache Camel]] |
| 5 | [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]] | SAGA coreografada (filas, `@RabbitListener`) e orquestrada (`SagaPedido` no Camel) |

## Ligações com outras disciplinas
- **Estrutura de Microsserviços (Fase 4)**: o [[Saga]] já aparecia nas queries com microsserviços (coreografia e orquestração, FIAP Store) e, na parte II, junto com Transaction Outbox e Event Sourcing.
- **Resiliência em Microsserviços (Fase 4)**: o [[Retry e Backoff Exponencial|Retry]] não resolve problemas de negócio, que pedem [[Transações Compensatórias]].
- **Arquitetura de Software (Fase 1)**: a [[Arquitetura Hexagonal]] do projeto de referência; os [[DAO e DTO|DTOs]] no pacote application.

## Dúvidas em aberto
- Aula 2: há duas Figuras 4, e a falha do orquestrador "vai **disponibilizar** toda a SAGA" (pelo contexto, indisponibilizar).
- Aula 3: na tabela da Pessimistic View, o saldo termina em 0, mas o saldo final é 100; o "O que você viu" chama o Reread Value de "Rever Valor".
- Aula 3: a tabela intercalada diz trazer "as mesmas SAGAS", mas começa com saldo 0 (a primeira, com 100); o exemplo de reler o status do pedido está no parágrafo da Pessimistic View.
- Aulas 4 × 5: as configurações ficam em `application.properties` na aula 4 e em `application.yml` na aula 5.
- Aula 4: o comando do Docker aparece com travessões e a porta como "5: 672".
- Aula 5: o texto diz que os pedidos seguem para "ORQUESTRAÇÃO_ENTREGA", mas o código os manda para `orquestracao_pagamentos`.

## Material
PDFs em `~/Desktop/SAGA Pattern /` ("Aula 1 - Padrão SAGA - Introdução.pdf" a "Aula 5 - Aplicando o padrão SAGA na prática - Parte II.pdf").
