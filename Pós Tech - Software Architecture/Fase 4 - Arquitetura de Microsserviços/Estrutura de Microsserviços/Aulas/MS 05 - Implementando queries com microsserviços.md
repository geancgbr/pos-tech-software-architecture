---
tags: [pos-tech/fase-4, microsservicos, aula]
disciplina: Estrutura de Microsserviços
aula: 5
fonte: "Estrutura de Microsserviços/Estrutura de Microsserviços - Aula 5.pdf"
---

# MS 05 - Implementando queries com microsserviços

← [[MS 04 - Modelo de API para microsserviços]] · [[Estrutura de Microsserviços]]

> [!summary] Em uma frase
> Com o **[[Banco de Dados por Serviço]]** (o banco compartilhado é um **anti-pattern** em microsserviços), consultas e transações entre serviços pedem novos padrões: **[[API Composition]]** (agregar chamadas, que podem ser paralelizadas), **[[CQRS]]** (com Event Handlers e as camadas Command e Query, alimentadas por **Domain Events**) e **[[Saga]]** (transações distribuídas por **coreografia** ou **orquestração**).

## Hands On
Implementar a **busca de produtos** agregando **Catálogo de Produtos, Precificação e Estoque**:
1. Instalar o **MySQL Workbench** (para ver os bancos de cada serviço) e o **Postman**. Configurar o MySQL de cada serviço com **scripts de migration** (bancos e usuários de serviço) e as **strings de conexão**.
2. Criar o serviço **Busca Produto** com **API Composition**, no endpoint **"Obter Produto"**, e testar com o Postman.
3. Adaptar para **CQRS**: uma migration para o banco **`busca_produto`**; o message broker **Amazon SQS** via **LocalStack**; Catálogo, Estoque e Precificação passam a **gerar eventos** de atualização no SQS; o Busca Produto os consome e **sincroniza** seu banco.
4. Testar a **replicação**: cadastros e atualizações refletidos no banco do Busca Produto.

## Arquitetura de banco de dados
| Padrão | O que é | Em microsserviços |
|---|---|---|
| **Banco de Dados Compartilhado** | Um banco **compartilhado** entre vários serviços; comum em **SOA** (Service-oriented Architecture) | Um **anti-pattern** (a evitar), por não garantir baixo acoplamento |
| **Banco de Dados por Serviço** | Um banco **dedicado** por serviço, sem compartilhamento; interação **só por APIs** síncronas ou assíncronas | **Baixo acoplamento**, mas mais complexidade em transações com dados em vários serviços, exigindo outros padrões, como **API Composition, CQRS e Saga** |

## Domain Event
- Criações e atualizações no domínio de um serviço **geram eventos** que representam as alterações, publicados, por exemplo, num **message broker** para os interessados. O **CQRS** e o **Saga** usam esse padrão. Ver [[Evento de Domínio]].

## API Composition
- Para **diminuir a latência**, **paralelizar** as chamadas: o **API Composer** dispara requisições **simultâneas** e agrega as respostas conforme chegam.
- Pela **facilidade de uso**, normalmente **damos preferência** ao API Composition; se os desafios dele inviabilizarem a operação, usar o **CQRS**.

## CQRS
É preciso implementar **Event Handlers** para os eventos de cada serviço, com atenção a:

| Característica | O que o PDF diz |
|---|---|
| **Idempotent Event Handlers** | Se pode haver **mensagens duplicadas** (sobretudo com garantia de entrega), o handler deve ser **idempotente**, mantendo o estado correto. Base: o **ID do evento** (já processado? fora de ordem, se incremental?) |
| **Consistência eventual** | Logo após um command, a query pode ainda **não estar sincronizada**. Para avisar o cliente, devolver o **ID da requisição** do command e enviá-lo na query: comparando os IDs, orienta-se o cliente a **aguardar** e repetir |
| **Reconstrução com eventos arquivados** | O broker **normalmente** tem um período de **retenção**, e eventos antigos são expurgados. Arquivar periodicamente os eventos num **storage** (ex.: **Amazon S3**) e combinar com os do broker para reconstruir a base de um **novo serviço** |
| **Reconstrução com snapshot** | Salvar periodicamente o **estado agregado** com o **ID do último evento**; reconstruir com o último snapshot + os eventos posteriores |

- **Carga full**: reconstrução **completa** a partir de outros serviços. **Carga delta**: só as mudanças recentes. Ao publicar um serviço novo, **normalmente** se faz **uma única carga full** e depois as **cargas delta**.

## Saga
- **Problema**: um pedido na FIAP Store envolve **decrementar o saldo do estoque** (para **reservar** o pedido), **validar o pagamento** e a **disponibilidade de transportadora**; numa transação **ACID** única, tudo faz commit ou rollback. Com **Pedido, Pagamento e Entrega** em serviços com bancos distintos (o PDF não cita o Estoque nessa lista), **é impossível** uma transação única.
- **Saga**: transações distribuídas como uma **sequência de transações locais**. Cada serviço que termina a sua dispara uma mensagem para a **próxima**; se uma falhar, o Saga executa **transações que revertem** as alterações.

| Forma | Como coordena |
|---|---|
| **Coreografia** | Cada transação local **dispara eventos** que acionam as de outros serviços; coordenação **cooperativa**, pelo interesse de cada serviço (Figura 1) |
| **Orquestração** | Um serviço com um **objeto orquestrador** diz aos outros quais transações executar; coordenação **centralizada** (Figura 2) |

## Referências
AWS: Amazon SQS · LocalStack · MySQL Workbench · Richardson, *Microservices Patterns* · Richardson: API Composition, CQRS, Saga · LocalStack Docs: SQS
