---
tags: [pos-tech/fase-4, microsservicos, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 1
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 1.pdf"
---

# MS2 01 - Desenhando a lógica de negócios com microsserviços

[[Estrutura de Microsserviços Parte II]] · Próxima → [[MS2 02 - Aplicando a lógica de negócios no microsserviço]]

> [!summary] Em uma frase
> Decompor o monolito em serviços e organizar a lógica de negócio com o padrão **transaction script**, numa estrutura de **[[Arquitetura Hexagonal]]**. O texto do PDF trata do **high-level domain model**, dos **desafios da decomposição** e do padrão **[[DAO e DTO|DAO]]** (Data Access Object). Segundo o resumo, a decomposição se faz por **capacidades de negócio** e **subdomínios DDD**.

## Hands On
- Analisar a estrutura do serviço **Catálogo de Produtos**, criado sob a **arquitetura hexagonal**: a classe **`CatalogoService`**, a lógica de negócio com **transaction script** e as **portas e adaptadores de entrada e saída**.
- Subir os containers de **MySQL** e **SQS** com **Docker Compose** e testar com o **Postman**.
- **Para rodar**: baixar o repositório da aula 1, instalar o **MySQL Workbench** (para ver o banco) e o **Postman**.
- Segundo o resumo, o transaction script organiza a lógica em **funções procedurais**.

## High-level domain model
Um **modelo de domínio de alto nível** mostra como os serviços se relacionam e contribuem para os **objetivos de negócio**: uma visão geral do que a organização tenta realizar e de como a tecnologia se encaixa.

| Importância | O que o PDF diz |
|---|---|
| **Compreensão do domínio** | Uma **linguagem comum** entendida de devs a stakeholders não técnicos |
| **Desacoplamento** | Responsabilidades claras por serviço |
| **Escalabilidade e manutenibilidade** | Interações delineadas e menos acoplamento |
| **Comunicação** | Ajuda a criar uma **[[Linguagem Ubíqua\|linguagem ubíqua]]** para toda a organização |

**Componentes típicos**: **entidades** (ex.: Cliente, Produto, Carrinho) · **serviços** (os microsserviços que lidam com as entidades e encapsulam as regras) · **relações** (composição, herança, associação) · **eventos** (ex.: finalizar uma compra **pode** desencadear um evento que faz o estoque atualizar a quantidade).

**Exemplo (e-commerce)**
- **Entidades**: Cliente, Produto, Carrinho, Pedido.
- **Microsserviços**: Serviço de Cliente, de Produto, de Carrinho, de Pedido.
- **Relações**: um Cliente pode ter um Carrinho; um Carrinho pode conter vários Produtos; um Pedido é feito por um Cliente e contém vários Produtos.
- **Eventos**: Produto Adicionado ao Carrinho, Pedido Finalizado, Produto Removido do Estoque.

## Desafios da decomposição
| Desafio | O que o PDF diz |
|---|---|
| **Domínios e limites** | Identificar corretamente os **limites dos domínios**; erros **podem levar** a **acoplamento forte** |
| **Granularidade** | Serviços muito **granulares** **podem levar** a overhead de comunicação; muito **abrangentes** **podem resultar** em baixa coesão e alta complexidade |
| **Comunicação** | Fica complexa rápido; escolher bem protocolos e padrões |
| **Transações e consistência** | Com cada serviço **podendo ter** seu banco, garantir **ACID** pode ser desafiador; padrões como **SAGA**, **Transaction Outbox** e/ou **Event Sourcing** |
| **Descoberta de serviços** | Soluções de descoberta e **load balancing** |
| **Segurança** | Cada serviço **pode precisar** de medidas próprias; gestão mais complexa |
| **Monitoramento e log** | Coletar e analisar logs e métricas de vários serviços |
| **Teste** | Testar em **isolamento** é simples; garantir o sistema inteiro é o desafio |
| **Implantação e DevOps** | CI/CD mais complexo, com pipelines e dependências por serviço |

## DAO (Data Access Object)
- Padrão que **abstrai e encapsula** as interações com a fonte de dados, **separando a lógica de negócio da de acesso aos dados**, para que evoluam de forma independente. Frequentemente associado a monolitos, mas relevante em microsserviços: cada serviço pode ter **seu banco e seus DAOs**.
- **Importância**: **desacoplamento** do esquema de armazenamento (fácil trocar de banco) · **reusabilidade** (código **DRY**, Don't Repeat Yourself) · **testabilidade** (testes unitários e de integração) · **consistência** nas operações **CRUD**.
- **Desafios**: **transações distribuídas** (projetar com **consistência eventual** ou **Saga**) · **padronização** dos DAOs entre os serviços.

## Referências
Cockburn, *Hexagonal architecture* (2005) · Fowler, Transaction Script · Oracle, Data Access Object · Richardson, *Microservices Patterns* · Richardson: Decompose by business capability · Decompose by subdomain
