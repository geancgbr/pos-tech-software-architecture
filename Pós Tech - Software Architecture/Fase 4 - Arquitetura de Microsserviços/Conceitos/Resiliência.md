---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Resiliência de sistemas, Defeito, erro e falha, Fault, Failure]
---

# Resiliência

Capacidade de **sistemas, processos e componentes** suportarem uma ampla variedade de **falhas**, mantendo a operação **total ou parcial**. É um **requisito crítico** ([[RES 01 - Introdução à resiliência]]). Resiliência **não significa eliminar falhas, mas reduzir seus impactos** ([[RES 03 - Resiliência na prática]]). Na aula 4, é a capacidade de se **recuperar de falhas e continuar operando normalmente** ([[RES 04 - Service Mesh e controle de tráfego]]).

> [!note] A aula 1 fala em manter a operação "total ou parcial"; a aula 4, em continuar operando "normalmente".

## Defeito, erro e falha ([[RES 01 - Introdução à resiliência]])
| Termo | Definição do PDF |
|---|---|
| **Defeito** | O software **não opera conforme as especificações**; todo defeito é causado por um **erro** |
| **Erro** | Comportamento inadequado que **pode** originar um defeito (valores incorretos, tempo excessivo) |
| **Falha** | A **causa raiz** do erro (design, implementação ou operação) |

> [!note] Na lista do PDF, defeito = **fault** e falha = **failure**; nos títulos das seções, os termos aparecem trocados.

## Tipos de defeitos ([[RES 01 - Introdução à resiliência]])
| Tipo | Como lidar |
|---|---|
| **Inconsistentes** (ex.: **Byzantine Failures**) | Clusters com protocolos de consenso (**Paxos**, **Raft**) |
| **Consistentes** | Normalmente **2n+1 réplicas** |
| **Fail-stop** | Normalmente **n+1 réplicas** |

## Resiliência × disponibilidade ([[RES 01 - Introdução à resiliência]])
- A **disponibilidade** é um indicador (solicitações com sucesso ou tempo funcional); a **resiliência** não é **apenas** um indicador, mas um **conjunto de estratégias e mecanismos** para mantê-la diante de falhas. Ver [[Disponibilidade e Observabilidade]] e [[MTTF, MTTR e MTBF]].
- **Mindset**: "O que pode dar errado com esta decisão ou implementação?". Práticas: programação defensiva, [[Chaos Engineering]], testes automatizados, redundância ([[Failover]]) e monitoramento contínuo.
- A base: **balanceamento de carga**, **health checks** e **escalabilidade horizontal** com auto-scaling.

## Padrões ([[RES 02 - Padrões de resiliência]])
[[Idempotência]] · [[Timeout]] · [[Retry e Backoff Exponencial]] · [[Circuit Breaker]] · [[Bulkhead]] · [[Rate Limiting e Throttling]] · [[Fallback e Graceful Degradation]] · [[Failover]]. Sistemas distribuídos **frequentemente** os combinam. Na prática: [[Resilience4j]] ([[RES 03 - Resiliência na prática]]); na infraestrutura: [[Service Mesh]] ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[RES 01 - Introdução à resiliência]], [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]], [[RES 04 - Service Mesh e controle de tráfego]], [[RES 05 - Chaos Engineering]]
