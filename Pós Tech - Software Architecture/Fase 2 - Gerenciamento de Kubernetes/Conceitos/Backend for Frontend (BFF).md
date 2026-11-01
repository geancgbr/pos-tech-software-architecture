---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [BFF, Backend-for-Frontend, Backend-to-Frontend]
---

# Backend for Frontend (BFF)

Criar **um grupo de APIs (backend) para cada tipo de cliente (frontend)**, em vez de uma interface genérica para todos.

- **Aula 5** ("Backend-to-Frontend"): por exemplo, três APIs, para navegadores web, Android e iOS. Cada uma trata as particularidades do seu cliente, sem complicar a interface com código de adaptação.
- **Aula 7**: com um endpoint único, o código da funcionalidade teria de descobrir o tipo de chamada e o formato do retorno. Com **um endpoint por cliente** (`/mobile/products` devolve só `name` e `identifier`; `/browser/products` devolve tudo), a decisão fica na **camada mais externa**, e o Controller não precisa de regra de negócio para isso.

Código do exemplo: [[CA 07 - Detalhes - dados, acesso e frameworks#Exemplo: Backend for Frontend (BFF)]]

## Na disciplina Estrutura de Microsserviços (Fase 4)
- Arquitetura cada vez mais usada com microsserviços: **um backend específico para cada interface de usuário (UI)**, que **agrega e formata** os dados de vários serviços e entrega **só o necessário** ([[MS 03 - Gerenciando API com API Gateway e BFF]]).
- **API Gateway dedicado** por cliente: uma squad responsável, escala dedicada ao cliente e custos mais previsíveis, instância mais leve, métricas e logs segmentados.
- **No Hands On**: o API Gateway do **App FIAP Store** no **Kong**.

Aparece em: [[CA 05 - Adaptadores de interface e frameworks e drivers]], [[CA 07 - Detalhes - dados, acesso e frameworks]], [[MS 03 - Gerenciando API com API Gateway e BFF]]
