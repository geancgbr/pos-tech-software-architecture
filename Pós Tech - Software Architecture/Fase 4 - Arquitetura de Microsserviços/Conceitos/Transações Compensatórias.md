---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Operação compensatória, Ação compensatória, Compensating transaction]
---

# Transações Compensatórias

Numa [[Saga]], em caso de falha, e **de acordo com o impacto para o negócio**, devem ser previstas operações compensatórias que **revertam** as operações já executadas até o ponto do problema ([[SAGA 01 - Introdução ao padrão SAGA]]).

| Operação | Compensatória (exemplo do PDF) |
|---|---|
| Reservar item estoque | **Cancelar reserva** |
| Criar registro contábil | **Criar registro reverso** |

- Se a **cobrança** falhar, a SAGA é interrompida e "Cancelar Reserva Estoque" é acionada.
- Assim como o **fluxo feliz**, as compensações **viáveis para o negócio** devem ser mapeadas no design do domínio.
- **Exemplo (seguros)**: em certos estágios, não se cancela a apólice; emite-se um **endosso de cancelamento**.
- Na aula 2, a Figura 1 mostra um trecho de SAGA com uma ação compensatória ([[SAGA 02 - Orquestração e coreografia]]); na aula 3, uma operação compensatória "devido à impossibilidade de cancelar" deixa o saldo negativo ([[SAGA 03 - Lidando com a falta do I do ACID]]).

Aparece em: [[SAGA 01 - Introdução ao padrão SAGA]], [[SAGA 02 - Orquestração e coreografia]], [[SAGA 03 - Lidando com a falta do I do ACID]]
