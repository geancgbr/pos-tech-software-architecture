---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Bulkhead Pattern, Compartimentos]
---

# Bulkhead

Inspirado nos **compartimentos de um navio**: isola partes do sistema, alocando recursos (**threads, conexões**) a grupos de operações, para que uma falha não **esgote todos os recursos** ([[RES 02 - Padrões de resiliência]]).

- Exemplo: threads para **pagamentos** e outras para **cadastro**.
- **Prós**: limita o impacto de falhas; facilita priorizar operações críticas. **Contras**: planejamento detalhado; **pode** desperdiçar recursos subutilizados.
- Combina com o [[Circuit Breaker]]: protege os recursos locais mesmo com o circuito "fechado" ([[RES 03 - Resiliência na prática]]). Implementado nas videoaulas com o [[Resilience4j]].

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]]
