---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Comunicação síncrona, Comunicação assíncrona, Mensageria, Message Broker, Broker de mensageria, Publish/subscribe, Point-to-point, Request/Response]
---

# Estilos de Comunicação entre Serviços

Para baixo acoplamento, **toda comunicação entre serviços é por API** ([[MS 02 - Comunicação entre processos com microsserviços]]).

| Tipo | Estilos |
|---|---|
| **One-to-one** | **Síncrono**: request/response (o cliente aguarda e pode ficar bloqueado). **Assíncrono**: request/response assíncrono (sem bloquear) e notificação one-way (sem resposta) |
| **One-to-many** (assíncrono) | **Publish/subscribe** (zero ou mais consumidores) e **publish/async response** (aguarda respostas por um período) |

- **API síncrona**: simples de implementar e testar, nativa, integra com proxy, firewall e balanceadores, sem intermediário. Mas: só request/response, **menor disponibilidade**, **lentidão propagada** e o cliente precisa **conhecer as URLs**.
- **Mensageria**: APIs assíncronas que **melhoram a disponibilidade**. Mensagem = **header** (metadados) + **body** (**documento, comando ou evento**). Canais **point-to-point** (um destinatário) e **publish-subscribe** (cópia para cada inscrito), num **message broker** como o **Apache Kafka**.
- **Na aula 5**: o **Amazon SQS** (via LocalStack) é o broker dos eventos do CQRS ([[MS 05 - Implementando queries com microsserviços]]).

Aparece em: [[MS 02 - Comunicação entre processos com microsserviços]], [[MS 05 - Implementando queries com microsserviços]]
