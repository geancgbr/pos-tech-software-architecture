---
tags: [pos-tech/fase-4, microsservicos, aula]
disciplina: Estrutura de Microsserviços
aula: 2
fonte: "Estrutura de Microsserviços/Estrutura de Microsserviços - Aula 2.pdf"
---

# MS 02 - Comunicação entre processos com microsserviços

← [[MS 01 - Estratégias e padrões de microsserviços]] · [[Estrutura de Microsserviços]] · Próxima → [[MS 03 - Gerenciando API com API Gateway e BFF]]

> [!summary] Em uma frase
> O primeiro microsserviço da FIAP Store, o **Estoque** (FastAPI + MySQL, com Docker Compose). Para baixo acoplamento, **toda comunicação é por API**, nos estilos **síncrono** e **assíncrono** (one-to-one e one-to-many). APIs síncronas são simples, mas reduzem a disponibilidade e propagam lentidão; o **[[Circuit Breaker]]** mitiga isso, a **[[Descoberta de Serviços]]** resolve a localização e a **mensageria** permite APIs assíncronas. Ver [[Estilos de Comunicação entre Serviços]].

## Hands On
Construir o primeiro microsserviço da **FIAP Store**, com materiais no **GitHub**. O Saiba Mais recapitula por escrito.

## O serviço Estoque
**1. Versão inicial (em memória)**: **FastAPI** em **Python**, com as operações "Obter Estoque", "Reservar Estoque" e "Debitar Estoque" pela **REST API** (Figura 1).
| Endpoint | O que faz |
|---|---|
| `GET /estoque/{sku}` | Devolve o produto (`em_estoque`, `reservado`) ou **404** "Produto não encontrado" |
| `POST /estoque/reserva` | Para cada operação (`sku`, `quantidade`): 404 se não existe; **400** "Estoque insuficiente" se a quantidade passa do estoque; senão, tira de `em_estoque` e soma em `reservado` |
| `POST /estoque/debito` | 404 se não existe; **400** se a quantidade passa do **reservado**; senão, tira de `reservado` |

- Estoque inicial do exemplo: SKU `"123"` = 10, `"456"` = 5, `"789"` = 2.
- `requirements.txt`: `fastapi==0.100.0`, `pydantic==2.0.2`, `uvicorn==0.22.0`.
- **Dockerfile**: `python:3.9-slim-buster`, instala as dependências, copia o `main.py`, **expõe a 8080** e inicia com o **uvicorn** (host `0.0.0.0`, porta `8080`).
- `docker build -t estoque .` → `docker run -it -p 8080:8080 estoque` → testar em `http://localhost:8080/estoque/456`.

**2. Com banco de dados dedicado (MySQL)**: **SQLAlchemy** (`mysql+mysqlconnector://user:password@db:3306/estoque`), tabela `estoque` (`sku` como chave, `em_estoque`, `reservado`) e dois endpoints novos:
| Endpoint | O que faz |
|---|---|
| `POST /estoque` | Cria o registro de estoque de um produto (com commit e rollback em caso de erro) |
| `PUT /estoque/{sku}` | Atualiza o registro |

- Os de reserva e débito passam a ler e atualizar no banco, numa sessão.
- `requirements.txt` ganha `mysql-connector-python==8.0.33` e `SQLAlchemy==2.0.18`.
- **docker-compose.yaml**: serviço `db` (`mysql:8.0`, banco `estoque`, volume `db_data`) e serviço `estoque` (build local, porta `8080`, `depends_on: db`).
- `docker-compose build` → `docker-compose up -d` → logs com `docker-compose logs -f estoque` (Ctrl+C para sair) → testes no **Postman**.

> [!note] O código completo está no PDF; aqui ficaram os endpoints e as regras. Na extração, o `CMD` do Dockerfile saiu embaralhado; os valores são `uvicorn main:app --host 0.0.0.0 --port 8080`.

## Estilos de comunicação
Toda comunicação por **APIs**, abstraindo a complexidade e garantindo **isolamento e independência**.

| Tipo | Estilo | Como funciona |
|---|---|---|
| **One-to-one, síncrono** | **Request/Response** | O cliente envia e **aguarda** resposta imediata, podendo ficar **bloqueado** |
| **One-to-one, assíncrono** | **Request/Response assíncrono** | O cliente envia e **não aguarda**; a resposta vem depois, **sem bloquear** |
| **One-to-one, assíncrono** | **Notificação one-way** | O cliente envia e **não espera** resposta |
| **One-to-many, assíncrono** | **Publish/subscribe** | Uma notificação consumida por **zero ou mais** serviços interessados |
| **One-to-many, assíncrono** | **Publish/async response** | Uma requisição, aguardando **por um período** as respostas dos interessados |

## Definindo uma API
- Perguntas: quais **operações** para cada cliente (Obter, Criar, Rastrear Pedido)? Qual **estilo** de comunicação? Quais **formatos** (JSON, XML, CSV)?

| API síncrona: benefícios | API síncrona: desafios |
|---|---|
| **Simples de implementar** (frameworks prontas) | **Só** request/response |
| **Fácil de testar** (navegador, Postman, curl) | **Menor disponibilidade**: cliente e serviço precisam estar disponíveis |
| Request/response **nativo** nas frameworks | **Lentidão propagada** ao cliente, que espera até o **timeout** |
| Integra fácil com **proxy, firewall, balanceadores** | O cliente precisa **conhecer o local** (URLs) dos serviços |
| **Sem componente intermediário** (broker) | — |

## Circuit Breaker
Ver [[Circuit Breaker]].
- Evita chamadas desnecessárias a serviços **degradados**, para sistemas **resilientes e autorrecuperáveis**, mitigando a **lentidão propagada** e o **efeito cascata**.

| Estado | O que acontece |
|---|---|
| **Fechado** | Chamadas normais. Se as falhas passam de um limite (ex.: **mais de 5 falhas em 2 minutos**), vai para **aberto** |
| **Aberto** | **Interrompe todas as chamadas**, dando tempo ao serviço para se recuperar. Depois de um tempo, vai para **semi-aberto** |
| **Semi-aberto** | Deixa passar **um número limitado** de chamadas: se dão certo, volta a **fechado**; se falham, volta a **aberto** |

- Os clientes **falham rápido**, em vez de esperar o timeout, indo para **cenários alternativos** (mensagem de erro, resultados parciais).

## Descoberta de Serviços
Ver [[Descoberta de Serviços]].
- Os serviços são **dinâmicos** (vários ambientes e servidores, sobretudo com **escala horizontal**).
- **Self registration**: ao iniciar, o serviço se registra num servidor de descoberta (geralmente o nome e a localização, como IP e porta; possivelmente outros metadados, como versão ou health check).
- **Service Registry**: consultado, geralmente, pelo **nome do serviço** (ex.: `estoque.fiapstore.com`) para saber como acessá-lo.
- **Sincronização**: o registry mantém a lista atualizada por **health checks** regulares ou permitindo que os serviços notifiquem quando estão saindo (**heartbeat**).

| Modelo | Como funciona |
|---|---|
| **Client-side** | O **cliente** consulta o registry e faz o **balanceamento de carga** |
| **Server-side** | O cliente passa por um **roteador intermediário**, que consulta o registry, roteia e pode balancear |

- Ferramentas comuns: **Consul, Etcd, Eureka (Netflix), Apache Zookeeper**.

## Disponibilidade
Indisponibilidade anual = (100% − disponibilidade) × 365 × 24. Ex.: com **99%**, **1% × 365 × 24 = 87,6 horas** por ano.

## API assíncrona com mensageria
- O padrão **Mensageria** implementa APIs assíncronas e **melhora a disponibilidade**, trocando interações síncronas por assíncronas.
- A **mensagem** tem **header** (metadados chave-valor: ID, data, índice para ordenação) e **body**: **documento** (só dados), **comando** (operações a executar) ou **evento** (uma mudança a ser entregue aos interessados). Ver a figura "Estrutura de uma Mensagem" (o PDF repete a numeração "Figura 1").

| Canal | Uso |
|---|---|
| **Point-to-point** | One-to-one assíncrono: **um único destinatário** processa a mensagem, mesmo com vários conectados |
| **Publish-subscribe** | One-to-many: **uma cópia** da mensagem para cada inscrito |

- Os canais são criados num **message broker**, como o **Apache Kafka**, que intermedeia a comunicação assíncrona e guarda as mensagens em **disco e/ou RAM**.

## Referências
Hohpe e Woolf, *Enterprise Integration Patterns* · Richardson, *Microservices Patterns* · Richardson: Circuit Breaker, Client-side service discovery, Messaging, Self Registration, Server-side service discovery, Service registry · AWS: What is an Application Load Balancer?
