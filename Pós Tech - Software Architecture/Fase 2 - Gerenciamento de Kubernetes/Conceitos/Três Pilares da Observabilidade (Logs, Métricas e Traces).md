---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Três pilares da observabilidade, Pilares da observabilidade, Telemetria, Sinais de telemetria]
---

# Três Pilares da Observabilidade (Logs, Métricas e Traces)

A observabilidade é construída sobre **três tipos de dados de telemetria**, que trabalham juntos para dar uma visão completa do sistema.

| Pilar | O que é | Quando usar | Back-end na disciplina |
|---|---|---|---|
| **Logs** | Registro de um **evento discreto** num ponto do tempo; a forma **mais antiga e granular** | Depuração detalhada, análise forense, fluxo de eventos num componente | [[Grafana Loki]] |
| **Métricas** | **Agregação numérica** ao longo do tempo; **leves e eficientes** | Saúde geral, tendências, dashboards, alertas | [[Prometheus]] |
| **Traces** | A **jornada completa de uma requisição** pelos serviços; uma coleção de **spans** | Latência de ponta a ponta, gargalos, dependências entre microsserviços | [[Jaeger]] |

- **Na narrativa de depuração da aula 5**, a **métrica** mostrou **o que** estava errado, o **trace** mostrou **onde** e o **log** mostrou **por quê**.

> [!note] Divergência entre aulas: a aula 3 diz que, a partir do dashboard de métricas, se mergulha nos **traces** "para entender onde e por quê". A aula 5 atribui o "por quê" ao **log**, e a aula 4 diz que o log pode dizer "exatamente por quê" uma operação demorou.
- **Correlação**: o **TraceId** nos logs liga os três pilares e é **o fio condutor** que costura todos os sinais ([[Logs Estruturados]]).
- **O valor** não está em cada pilar isolado, mas na **sinergia e na correlação** entre eles: não é ter "três ferramentas separadas".
- **Quarto pilar** (tendência): o **continuous profiling** ([[Tendências da Observabilidade (eBPF, Profiling e AIOps)]]).

Monitoramento × observabilidade: [[Disponibilidade e Observabilidade#Na disciplina OpenTelemetry (Fase 2)]].

## Na disciplina Resiliência em Microsserviços (Fase 4)
No Chaos Engineering: **métricas** para tendências e baselines, **logs** para a sequência de eventos e **traces** para ver onde as falhas se propagam; mais instrumentação, correlação (trace IDs), visualização e alertas inteligentes ([[RES 05 - Chaos Engineering]]).

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]], [[OTEL 04 - OpenTelemetry Logs (Loki)]], [[OTEL 05 - Boas práticas e desafios]], [[RES 05 - Chaos Engineering]]
