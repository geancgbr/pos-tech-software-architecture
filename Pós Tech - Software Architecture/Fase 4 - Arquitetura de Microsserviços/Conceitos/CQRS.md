---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Command Query Responsibility Segregation, Event Handler, Event Handlers, Consistência eventual, Carga full, Carga delta]
---

# CQRS

O PDF não define o CQRS: descreve as camadas **Command** e **Query**, os **Event Handlers** que processam os **eventos** ([[Evento de Domínio|Domain Events]]) dos outros serviços e, no Hands On, o Busca Produto com **banco próprio** sincronizado por eventos ([[MS 05 - Implementando queries com microsserviços]]).

- **Event Handlers**: processam os eventos recebidos. Cuidados:
  - **Idempotência**: mensagens duplicadas não podem corromper o estado (usar o **ID do evento**).
  - **Consistência eventual**: a query pode estar atrasada; devolver o **ID da requisição** do command e compará-lo na query.
  - **Reconstrução com eventos arquivados** (ex.: no **Amazon S3**), já que o broker normalmente tem retenção.
  - **Reconstrução com snapshot**: último estado agregado + eventos posteriores ao ID registrado.
- **Carga full** (reconstrução completa) × **carga delta** (só as mudanças); num serviço novo, normalmente uma full e depois as delta.
- **No Hands On**: Catálogo, Estoque e Precificação publicam eventos no **Amazon SQS** (LocalStack), e o **Busca Produto** sincroniza o banco `busca_produto`.
- Usar quando o [[API Composition]] for inviável.

Aparece em: [[MS 05 - Implementando queries com microsserviços]]
