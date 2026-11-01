---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Database per Service, Banco de Dados Compartilhado, Shared Database]
---

# Banco de Dados por Serviço

| Padrão | Em microsserviços |
|---|---|
| **Banco de Dados Compartilhado** | Comum em **SOA**, mas um **anti-pattern** em microsserviços, por não garantir baixo acoplamento |
| **Banco de Dados por Serviço** | Um banco **dedicado** por serviço, acessado só pela sua API: **baixo acoplamento**, mas exige outros padrões, como [[API Composition]], [[CQRS]] e [[Saga]], para dados distribuídos |

- Na aula 1, cada serviço tem seu banco **logicamente** dedicado; não precisa de uma instância física própria ([[MS 01 - Estratégias e padrões de microsserviços]]).
- Na disciplina Data Engineering: "banco de dados por serviço" como implicação dos microsserviços ([[DE 07 - Bancos de dados e microsserviços]]).

Aparece em: [[MS 01 - Estratégias e padrões de microsserviços]], [[MS 05 - Implementando queries com microsserviços]], [[DE 07 - Bancos de dados e microsserviços]]
