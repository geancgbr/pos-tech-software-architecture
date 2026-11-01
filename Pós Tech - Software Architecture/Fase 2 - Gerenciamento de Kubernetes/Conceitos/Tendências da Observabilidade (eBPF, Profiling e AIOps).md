---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [eBPF, Continuous profiling, Profiling contínuo, AIOps, Flame graph, Pyroscope]
---

# Tendências da Observabilidade (eBPF, Profiling e AIOps)

| Tendência | O que é | Na observabilidade |
|---|---|---|
| **eBPF** (Extended Berkeley Packet Filter) | Tecnologia **no kernel do Linux** que roda programas num **sandbox** no kernel, sem alterar o código dele nem carregar módulos | Agentes eBPF **podem observar** chamadas de sistema, rede e interações entre processos, coletando métricas, traces e logs (como dados **RED**: Rate, Errors, Duration) **sem instrumentar o código**. **Cilium** e **Pixie** (da New Relic) exportam em **OTLP**. Futuro provável: **eBPF** para infraestrutura e rede + **OTel** para o contexto de negócio |
| **Continuous profiling** (o **quarto pilar**) | Analisa constantemente **CPU e alocação de memória** em produção, **até a linha** do código | O trace diz que o span é lento; o profiler diz **qual função e linha** consome 80% da CPU. Visualização em **flame graphs**. Back-end de exemplo: **Pyroscope** (fundido com o **Grafana Phlare**). O OTel trabalha para padronizar um modelo de dados de profiles |
| **AIOps** | **Machine Learning e IA** aplicados aos dados de observabilidade | **Detecção de anomalias**, **correlação de eventos** (causa raiz provável) e **análise preditiva**. O OTel, com dados estruturados e padronizados, é a fonte ideal |

## Na disciplina Resiliência em Microsserviços (Fase 4)
Como tendência de Service Mesh, o **eBPF** executa código seguro no kernel Linux; meshes baseados nele, como o **Cilium**, reduzem o overhead ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[OTEL 05 - Boas práticas e desafios]], [[RES 04 - Service Mesh e controle de tráfego]]
