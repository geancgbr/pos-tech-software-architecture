---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [DAO, Data Access Object, DTO, Data Transfer Object, ORM, Object-Relational Mapping]
---

# DAO e DTO

| | DAO (Data Access Object) | DTO (Data Transfer Object) |
|---|---|---|
| O que é | Abstrai e encapsula as interações com a **fonte de dados**, separando a lógica de negócio da de acesso | **Transfere dados** entre componentes; em microsserviços, **frequentemente** estrutura as **mensagens** entre serviços |
| Vantagens | **Desacoplamento** do esquema · **reusabilidade** (DRY) · **testabilidade** · **consistência** no CRUD | **Desacoplamento** do modelo de domínio de outros serviços · **eficiência** na serialização · **validação** |
| Desafios (DAO) / Desvantagens (DTO) | **Transações distribuídas** (consistência eventual, Saga) · **padronização** entre serviços | **Mapeamento** domínio ↔ DTO · **manutenção** quando o modelo muda |
| Aula | [[MS2 01 - Desenhando a lógica de negócios com microsserviços]] | [[MS2 02 - Aplicando a lógica de negócios no microsserviço]] |

## ORM (Object-Relational Mapping)
Técnica que mapeia objetos do domínio para um banco relacional ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]).
- **Vantagens**: abstração (objetos em vez de SQL) · desacoplamento do esquema · produtividade (migrações, sessão) · consistência com o modelo de domínio (útil no DDD).
- **Desvantagens**: performance em operações complexas · acoplamento à biblioteca · transações distribuídas (Saga).

## Na disciplina SAGA Pattern (Fase 4)
No projeto de referência, os dados transitam entre a aplicação e o mundo externo através dos **DTOs**, no pacote **application** ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).

Aparece em: [[MS2 01 - Desenhando a lógica de negócios com microsserviços]], [[MS2 02 - Aplicando a lógica de negócios no microsserviço]], [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]
