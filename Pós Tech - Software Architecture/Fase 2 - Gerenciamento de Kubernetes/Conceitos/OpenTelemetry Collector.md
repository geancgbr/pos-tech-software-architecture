---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [OTel Collector, Collector, Coletor, OTLP, OpenTelemetry Protocol]
---

# OpenTelemetry Collector

**Serviço de proxy (agente)** que roda junto da aplicação ou num host separado. **Recebe** telemetria de várias fontes, pode **processá-la** (adicionar atributos, filtrar dados sensíveis) e **exportá-la** para um ou mais back-ends. O formato nativo do OTel é o **OTLP (OpenTelemetry Protocol)**.

**Por que usar** (boa prática em produção)
| Vantagem | O que o PDF diz |
|---|---|
| **Desacoplamento** (a principal) | As aplicações só falam **OTLP**. Migrar do Jaeger ou adicionar outro back-end muda **só a configuração do Coletor**, sem alterar código nem fazer deploy |
| **Gerenciamento centralizado** | Centraliza a configuração de exportação. O Prometheus só precisa saber o endereço dos coletores |
| **Processamento centralizado** | **Amostragem tail-based**, **filtragem de PII** (LGPD/GDPR), **enriquecimento de metadados** (região, ID do cluster Kubernetes, versão) e **eficiência de rede** (lotes) |

**Nas aulas**
- **Traces**: recebe os spans via OTLP, **pode processar** (amostragem, atributos) e exporta com o **jaeger exporter** ([[OTEL 02 - OpenTelemetry Tracing (Jaeger)]]).
- **Métricas**: como **ponte para o Prometheus**, com o **Prometheus Exporter** expondo `/metrics`. No **modo reverso**, um **Prometheus Receiver** raspa alvos existentes e converte para OTLP. Essa flexibilidade o torna **a peça central** de qualquer estratégia moderna de telemetria ([[OTEL 03 - OpenTelemetry Metrics (Prometheus)]]).
- **Logs**: segundo o resumo da aula 4, uma pipeline de logs com o Coletor e o Loki ([[OTEL 04 - OpenTelemetry Logs (Loki)]]).
- **Na aula 5** ([[OTEL 05 - Boas práticas e desafios]]):
  - **Overhead**: implantar como **agente em cada nó** (**DaemonSet** no Kubernetes) em vez de um deployment centralizado.
  - **Custo**: **filtrar** dados de baixo valor (logs de DEBUG em produção, métricas de health checks).
  - **Código legado**: se tudo mais falhar, analisar **logs de acesso** e gerar métricas a partir deles.

Os outros componentes da arquitetura (**API, SDK e Exporters**): [[OpenTelemetry#A arquitetura]].

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]] a [[OTEL 05 - Boas práticas e desafios]]
