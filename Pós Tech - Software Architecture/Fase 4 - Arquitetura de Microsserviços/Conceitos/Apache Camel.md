---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Camel]
---

# Apache Camel

Usado no projeto de referência para **orquestrar** os passos da [[Saga]] ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]). Nada impede implementar o orquestrador **manualmente**, mas há soluções que **podem** facilitar o processo e simplificar a manutenção.

- Dependências `camel-spring-boot-starter` e `camel-spring-rabbitmq-starter` (versão **4.1.0**); a classe `SagaPedido` define rotas `from(...)` → `.to(...)` sobre o [[RabbitMQ]], com `.choice().when(...)` ([[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).
- Alternativas de orquestração: **Eventuate Tram, IBM App Connect, Mule Soft (ESB), AWS Step Functions, Google Cloud Application Integration** ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).

Aparece em: [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]
