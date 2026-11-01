---
tags: [pos-tech/fase-4, microsservicos, indice]
disciplina: Estrutura de Microsserviços
fase: 4
aulas: 5
---

# Estrutura de Microsserviços

[[Fase 4 - Arquitetura de Microsserviços]] · Revisão → [[Revisão - Estrutura de Microsserviços]]

> [!note] Os PDFs não trazem nome de autor. Todas as aulas usam a aplicação fictícia **FIAP Store**, refatorada de monolito para microsserviços, com materiais num link do GitHub.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[MS 01 - Estratégias e padrões de microsserviços]] | [[Arquitetura Monolítica]], [[Arquitetura de Microsserviços]] |
| 2 | [[MS 02 - Comunicação entre processos com microsserviços]] | [[Estilos de Comunicação entre Serviços]], [[Circuit Breaker]], [[Descoberta de Serviços]] |
| 3 | [[MS 03 - Gerenciando API com API Gateway e BFF]] | [[API Gateway]], [[Backend for Frontend (BFF)]], [[API Composition]], [[Kong]] |
| 4 | [[MS 04 - Modelo de API para microsserviços]] | [[Modelagem de APIs]] |
| 5 | [[MS 05 - Implementando queries com microsserviços]] | [[Banco de Dados por Serviço]], [[CQRS]], [[Saga]], [[Evento de Domínio]] |

## A FIAP Store ao longo das aulas
| Aula | O que acontece |
|---|---|
| 1 | Tabela de serviços, operações e integrações |
| 2 | O serviço **Estoque** em FastAPI, depois com MySQL e Docker Compose |
| 3 | O **Kong** como API Gateway do App (BFF), com self-register e Basic Auth |
| 4 | O **contrato OpenAPI** da API "FIAP Store – Website" no Swagger |
| 5 | O serviço **Busca Produto**, com API Composition e depois CQRS (SQS no LocalStack) |

A tabela é só um mapa de navegação, montado a partir dos Hands On.

## Ligações com outras disciplinas
- **API Gateway (Fase 3)**: o [[Kong]] e o [[API Gateway]] já tinham aparecido lá.
- **Clean Architecture (Fase 2)**: o [[Backend for Frontend (BFF)|BFF]] e a [[Arquitetura Monolítica]].
- **DDD (Fase 1)**: o [[Evento de Domínio]] reaparece como padrão **Domain Event**.
- **Data Engineering (Fase 4)**: microsserviços e bancos de dados em [[DE 07 - Bancos de dados e microsserviços]].
- **Dockerização (Fase 2)**: o Estoque sobe com [[Docker Compose]].

## Material
PDFs em `~/Desktop/Estrutura de Microsserviços/` ("Estrutura de microsserviços - Aula 1.pdf" a "Aula 5.pdf").
