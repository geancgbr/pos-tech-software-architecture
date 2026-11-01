---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Rabbit MQ]
---

# RabbitMQ

Solução de **mensageria** muito popular, usada no projeto de referência para integrar os serviços de forma **assíncrona e desacoplada** ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).

```bash
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.12-management
```
- Porta **5672**: integração com os serviços; **15672**: console web administrativo; credenciais padrão **guest/guest** ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).
- Na SAGA coreografada: filas `pedidos`, `entregas_confirmadas`, `pagamentos_confirmados`, `pagamentos_pendentes`; dependência `spring-boot-starter-amqp`; `RabbitTemplate.convertAndSend` para publicar e `@RabbitListener` para escutar ([[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).
- Na orquestrada: exchange **`demo`** e filas `orquestracao_*`, usadas pelo [[Apache Camel]] ([[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).
- Alternativas citadas: **Kafka, Google Cloud Pub/Sub, Amazon SQS, Azure Service Bus** ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).

Aparece em: [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]
