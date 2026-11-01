---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Domain Event, Eventos de Domínio, Evento Pivotal, Eventos Pivotais]
---

# Evento de Domínio

**Algo que aconteceu no domínio.** Por isso se escreve **no passado**: "Atividade entregue", "Nota gravada".

- É gerado por um **comando**, que vem de um ator ou de uma **política**.
- **Evento pivotal**: marca uma troca de fase ou de contexto no fluxo. Indica fortemente o limite de um [[Contexto Delimitado]].

## Na disciplina Estrutura de Microsserviços (Fase 4)
O padrão **Domain Event**: criações e atualizações no domínio de um serviço **geram eventos** publicados, por exemplo, num **message broker**, para os serviços interessados. O [[CQRS]] e o [[Saga]] usam esse padrão ([[MS 05 - Implementando queries com microsserviços]]).

Aparece em: [[DDD 06 - Event Storming]], [[MS 05 - Implementando queries com microsserviços]]
