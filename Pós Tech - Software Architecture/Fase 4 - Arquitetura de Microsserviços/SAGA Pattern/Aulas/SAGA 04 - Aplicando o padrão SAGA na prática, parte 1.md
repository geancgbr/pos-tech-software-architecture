---
tags: [pos-tech/fase-4, microsservicos, saga, aula]
disciplina: SAGA Pattern
aula: 4
fonte: "SAGA Pattern/Aula 4 - Aplicando o padrão SAGA na prática - Parte I.pdf"
---

# SAGA 04 - Aplicando o padrão SAGA na prática, parte 1

← [[SAGA 03 - Lidando com a falta do I do ACID]] · [[SAGA Pattern]] · Próxima → [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]

> [!summary] Em uma frase
> Apresenta o **projeto de referência**: **3 serviços** da FIAP Store (**pedido, cobrança e entrega**) em **Java + Spring Boot**, **Maven**, banco **H2** e estilo **hexagonal**; o **RabbitMQ** para a mensageria e o **Apache Camel** para a orquestração. A SAGA é **agnóstica à tecnologia**.

## Hands On (vídeo)
Na videoaula: o projeto que será usado como referência para implementar exemplos de SAGAs.

## Projeto de referência
- **3 serviços** (Figura 1): `fiapstore-pedido-service`, `fiapstore-cobranca-service` e `fiapstore-entrega-service`.

| Tecnologia | Escolha |
|---|---|
| Linguagem | **Java** |
| Framework | **Spring Boot** |
| IDE | **IntelliJ IDEA 2023.1.3** |
| Gerenciador de pacotes | **Maven** |
| Banco de dados | **H2** |
| Estilo arquitetural | **Hexagonal** ([[Arquitetura Hexagonal]]) |

- "O estilo arquitetural **não tem relação com as pastas**", mas as principais estruturas são mostradas (Figura 2). Em geral, todos os serviços seguem a mesma estrutura:

| Pacote | Conteúdo |
|---|---|
| **domain** (o mais importante; Figura 3) | **Entidades de domínio** com as regras de negócio e **Exceptions customizadas**; as pastas **repository** e **usecase** guardam as **interfaces ou "portas"** para interagir com as entidades |
| **application** (Figura 4) | O que permite interagir com a aplicação, toda por **API REST**: a classe **controller** expõe os endpoints; os dados transitam pelos **DTOs** ([[DAO e DTO]]); o pacote **usecase** concentra "nossos casos ou nossos **adaptadores de entrada**" (frase truncada no PDF) |
| **infra** (Figura 5) | **Adaptadores de saída**; inicialmente, só o banco de dados |

## Bancos de dados
- **H2**, muito comum para **demonstração**, com **persistência em arquivo**:
  `jdbc:h2:file:D:/_dev_ssd/databases_demo/pedidoDB;mode=PostgreSQL;AUTO_SERVER=TRUE`
- `AUTO_SERVER=TRUE` permite **múltiplas conexões**, o que possibilita executar queries **durante o serviço**.
- Estruturas: MER do **pedido-service** (Figura 6; os dados da tabela **produto** são carregados automaticamente por `src/main/resources/data.sql`); tabela **Entrega_Entity** (Figura 7); tabela **Pagamento_Entity** (Figura 8). Os outros bancos têm **uma tabela cada**.
- O banco é **transparente** para a aplicação: pode-se usar o relacional que preferir.

## Swagger e testes
| Serviço | Documentação Swagger |
|---|---|
| fiapstore-pedido-service | `localhost:8081/doc` |
| fiapstore-cobranca-service | `localhost:8082/doc` |
| fiapstore-entrega-service | `localhost:8083/doc` |

- Portas e configurações em `src/main/resources/application.properties` (Figura 9: Swagger).

> [!note] Aqui as configurações ficam em `application.properties`; na aula 5, filas e conexão são registradas em `application.yml`.
- Cada endpoint tem um **payload de exemplo** (Figura 10); o **CPF** é fake, do **Gerador de CPF – 4Devs**.
- Cada serviço tem um **conjunto mínimo de testes**, para garantir que tudo continue funcionando depois das implementações (Figuras 11 a 13: PedidoController, EntregaController, PagamentoController).

## Mensageria: RabbitMQ
- Integração **assíncrona e desacoplada** com o **RabbitMQ**; para simplificar, ele **pode** ser executado via Docker. Ver [[RabbitMQ]].
```bash
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.12-management
```
- Integração com os serviços pela porta **5672**; a **15672** é a do **console web administrativo** (Figuras 14 e 15). Credenciais padrão: **guest/guest**.
- Será usado **só o indispensável**; nada impede outras soluções, como **Kafka, Google Cloud Pub/Sub ou Amazon SQS**.

> [!note] Nesta aula, o comando aparece com travessões ("–rm –name") e a porta como "5: 672"; a forma correta, que aparece na aula 5, é `--rm --name` e **5672**.

## Orquestração: Apache Camel
- Nada impede implementar o orquestrador **manualmente**, mas há soluções que facilitam e simplificam a manutenção. Será usado o **Apache Camel**; alternativas: **Eventuate Tram, IBM App Connect, Cloud Application Integration**, entre outras. Ver [[Apache Camel]].

## Para saber mais
A SAGA é **agnóstica à tecnologia**. Alternativas:

| Orquestração | Mensageria |
|---|---|
| **IBM App Connect** (integração de aplicativos) · **Mule Soft** (Enterprise Service Bus) · **AWS Step Functions** · **Google Cloud Application Integration** · **Eventuate Tram** | **Amazon Simple Queue Service** · **Google Cloud Pub/Sub** · **Apache Kafka** · **Azure Service Bus** |

## Referências
Apache Camel User Manual · RabbitMQ: página oficial · Richardson, *Microservices Patterns*
