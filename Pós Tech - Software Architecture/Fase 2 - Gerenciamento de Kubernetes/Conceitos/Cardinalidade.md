---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Alta cardinalidade, Explosão de cardinalidade, Cardinality]
---

# Cardinalidade

O **número de valores únicos** de um atributo (ou label, no Prometheus e no Loki). A **alta cardinalidade** é **um dos maiores desafios técnicos e de custo** em observabilidade.

- **O problema**: cada combinação única de labels cria uma **nova série temporal** (Prometheus) ou um **novo fluxo** a indexar (Loki). Atributos de cardinalidade infinita (`user_id`, `request_id`, `trace_id`) como labels causam uma **"explosão de cardinalidade"**, que pode **derrubar o back-end**.

| Onde | Regra |
|---|---|
| **Métricas (Prometheus)** | **Nunca** usar alta cardinalidade como label; usar `http_method`, `status_code_class` (2xx, 4xx, 5xx), `service_version` |
| **Logs (Loki)** | Labels para infraestrutura (cluster, namespace, pod, service) e severidade; `user_id` e `trace_id` **no corpo** |
| **Traces (Jaeger)** | **Projetados para alta cardinalidade**: `user_id` pode ir nos spans |

Aparece em: [[OTEL 05 - Boas práticas e desafios]]
