---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Retry, Retry Pattern, Retentativa, Backoff exponencial, Jitter]
---

# Retry e Backoff Exponencial

Repetir uma requisição diante de **falha temporária**; exige **[[Idempotência]]** ([[RES 02 - Padrões de resiliência]]).

| Estratégia ([[RES 02 - Padrões de resiliência]]) | Resumo |
|---|---|
| **Imediatos em memória** | **Geralmente** na mesma thread; número máximo de tentativas (ex.: HTTP 503) |
| **Assíncronos** | Desacoplam; ex.: **202 Accepted** em vez de 201 Created; alternativa de fallback |
| **Backoff exponencial** | Espera crescente (1 s, 2 s, 4 s, 8 s, 16 s...) |

- **Jitter**: aleatoriedade somada à espera, para evitar que vários clientes repitam **sincronizados**. Exemplo em Node.js: 5 tentativas, base 500 ms ([[RES 03 - Resiliência na prática]]).
- **Boas práticas do Retry Pattern** ([[RES 04 - Service Mesh e controle de tráfego]]): **número máximo de retentativas, backoff exponencial, jitter e idempotência**. No **Service Mesh**, o **Control Plane** configura o número de retentativas, o **tempo limite**, o backoff e o jitter.

## Na disciplina SAGA Pattern (Fase 4)
O **Retry** define novas tentativas e intervalos, mas não resolve problemas **de negócio** (ex.: cartão cancelado, transportadora sem entregar); daí a [[Saga]] com [[Transações Compensatórias]] ([[SAGA 01 - Introdução ao padrão SAGA]]).

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]], [[RES 04 - Service Mesh e controle de tráfego]], [[SAGA 01 - Introdução ao padrão SAGA]]
