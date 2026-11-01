---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Padrão Saga, Coreografia, Orquestração, Transações distribuídas]
---

# Saga

Padrão para **transações distribuídas** entre serviços com bancos distintos, como uma **sequência de transações locais** ([[MS 05 - Implementando queries com microsserviços]]).

- Cada serviço que termina sua transação local dispara uma mensagem para a **próxima**. Se uma falha, o Saga executa **transações que revertem** as anteriores, garantindo a consistência.
- **Exemplo**: um pedido na FIAP Store (estoque, pagamento, transportadora) com **Pedido, Pagamento e Entrega** em serviços separados, onde uma transação **ACID** única é impossível.

| Coordenação | Como |
|---|---|
| **Coreografia** | Eventos de cada transação acionam as dos outros serviços; **cooperativa** |
| **Orquestração** | Um **orquestrador** num serviço diz o que cada um executa; **centralizada** |

- Usa o padrão **Domain Event** ([[Evento de Domínio]]).

## Na disciplina Estrutura de Microsserviços Parte II
Com cada serviço **podendo** ter seu próprio banco, garantir transações ACID **pode** ser desafiador, sendo necessários padrões como **SAGA**, **Transaction Outbox** e/ou **Event Sourcing** ([[MS2 01 - Desenhando a lógica de negócios com microsserviços]]). O Saga também aparece nos desafios do DAO ([[MS2 01 - Desenhando a lógica de negócios com microsserviços]]) e nas desvantagens do ORM ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]).

## Na disciplina SAGA Pattern (Fase 4)
- **Origem**: paper de **Hector Garcia-Molina e Kenneth Salem** (1987), contra os **locks** no banco que prejudicavam a velocidade ([[SAGA 01 - Introdução ao padrão SAGA]]). Ver [[XA (Extended Architecture)]].
- **Definição**: uma **sequência de transações locais coordenadas através de mensagens**; cada serviço é um **participante** com transações locais [[ACID]]; a SAGA oferece controle **ACD, e não ACID**, com [[Transações Compensatórias]] ([[SAGA 01 - Introdução ao padrão SAGA]]).
- **Coreografia** × **orquestração** ([[SAGA 02 - Orquestração e coreografia]]):

| | Coreografia | Orquestração |
|---|---|---|
| Quem decide | Distribuído entre os participantes (eventos) | Um **orquestrador** envia **comandos** |
| Prós | Simplicidade · acoplamento fraco | Dependências simplificadas (mão única) · acoplamento fraco · lógica centralizada |
| Contras | Mais difícil de entender · dependências cíclicas · risco de forte acoplamento | Orquestrador complexo · **ponto único de falha** |

- Segundo **Chris Richardson**, a coreografia é mais recomendada para **SAGAs simples**; nos demais cenários, a orquestração **tende** a ser mais benéfica ([[SAGA 02 - Orquestração e coreografia]]). Em nuvem: **Google Cloud Workflows** e **AWS Step Functions**.
- A falta do isolamento **pode** gerar [[Anomalias de Dados em Sagas]] ([[SAGA 03 - Lidando com a falta do I do ACID]]).
- **Na prática**: serviços de pedido, cobrança e entrega em Java/Spring Boot, com [[RabbitMQ]] e [[Apache Camel]]; a orquestrada é **mais fácil de entender**, mas a indisponibilidade do serviço de pedidos **poderia** parar todo o processamento ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).
- O padrão é **agnóstico à tecnologia**; os fluxos devem ser validados no design, com diagramas versionados ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).

Aparece em: [[MS 05 - Implementando queries com microsserviços]], [[MS2 01 - Desenhando a lógica de negócios com microsserviços]], [[MS2 02 - Aplicando a lógica de negócios no microsserviço]], [[SAGA 01 - Introdução ao padrão SAGA]], [[SAGA 02 - Orquestração e coreografia]], [[SAGA 03 - Lidando com a falta do I do ACID]], [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]
