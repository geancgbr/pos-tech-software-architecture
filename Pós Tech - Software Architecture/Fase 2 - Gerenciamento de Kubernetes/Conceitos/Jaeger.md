---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [jaeger, Jaeger UI, Jaeger Collector, Jaeger Query]
---

# Jaeger

Projeto **de código aberto**, **graduado pela CNCF**, criado na **Uber** para **tracing distribuído**: **armazenar, encontrar e visualizar traces**. Pode ser implantado de diferentes maneiras, desde **"all-in-one"** (local) até uma arquitetura escalável (produção).

| Componente | Papel |
|---|---|
| Jaeger Client (**obsoleto**) | Hoje: **SDK do OpenTelemetry + exportador OTLP** |
| **Jaeger Collector** | Recebe, valida, indexa e armazena |
| **Storage Back-end** | **Não tem armazenamento próprio**; as opções mais comuns são Elasticsearch e Cassandra |
| **Jaeger Query** | API de busca |
| **Jaeger UI** | Interface web de pesquisa e visualização |

**Fluxo**: aplicação (SDK OTel) → OTLP → [[OpenTelemetry Collector|OTel Collector]] → jaeger exporter → Jaeger Collector → storage → Jaeger UI.

- **Na aula 4**: o Grafana cria um link direto de cada linha de log para o trace correspondente no Jaeger.
- **Na aula 5**: a visualização **em cascata (Gantt chart)** mostra o gargalo. O texto fala em "UI do Jaeger ou Grafana Tempo".

Aparece em: [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]], [[OTEL 04 - OpenTelemetry Logs (Loki)]], [[OTEL 05 - Boas práticas e desafios]]
