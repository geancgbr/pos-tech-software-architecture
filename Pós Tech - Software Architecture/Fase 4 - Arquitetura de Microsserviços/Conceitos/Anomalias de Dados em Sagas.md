---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Lost Updates, Atualizações perdidas, Dirty Reads, Leituras sujas, Pessimistic View, Visão pessimista, Reread Value, Reler valor]
---

# Anomalias de Dados em Sagas

**Possíveis** consequências da falta de **isolamento** ([[ACID]]) em SAGAs ([[SAGA 03 - Lidando com a falta do I do ACID]]).

| Anomalia | Definição | Impacto no exemplo | Contramedida |
|---|---|---|---|
| **Lost Updates** | Uma SAGA **sobrescreve, sem ler**, as alterações de outra | O cliente recebe um pedido que deveria ter sido **cancelado** | **Reread Value**: reler os dados antes de atualizar; se mudaram, **abortar** |
| **Dirty Reads** | Uma transação ou SAGA **lê as atualizações** de outra ainda **incompleta** | O cliente usou **mais pontos** do que tinha (saldo −100) | **Pessimistic View**: reordenar os passos para ler só depois de todas as atualizações (ex.: restituir os pontos **depois** de cancelar a entrega) |

- A Pessimistic View **pode** ser eficaz contra Dirty Reads, mas **pode** aumentar a complexidade e reduzir o desempenho.
- Ver [[Níveis de Isolamento de Transações]].

> [!note] No "O que você viu" da aula, o Reread Value é chamado de "Rever Valor".

Aparece em: [[SAGA 03 - Lidando com a falta do I do ACID]]
