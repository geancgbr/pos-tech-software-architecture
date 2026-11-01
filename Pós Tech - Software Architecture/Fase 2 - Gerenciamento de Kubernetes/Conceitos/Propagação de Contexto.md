---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Context propagation, W3C Trace Context, traceparent, tracestate, B3 Propagation, B3]
---

# Propagação de Contexto

O mecanismo que faz o **TraceId e o SpanId** viajarem de um serviço para outro. O **contexto (Context)** é um objeto do OTel com o TraceId e o SpanId do span ativo. A propagação o **serializa**, envia pela rede (geralmente em **cabeçalhos**) e **desserializa** no receptor.

1. **Injeção** (cliente): o SDK injeta o contexto nos metadados da requisição.
2. **Extração** (servidor): o SDK extrai o contexto.
3. **Span filho**: com o TraceId e o ParentSpanId, o receptor cria um span ligado como filho.

| Padrão | Cabeçalhos |
|---|---|
| **W3C Trace Context** (**recomendado** pelo OTel; padrão oficial da W3C) | **`traceparent`** (versão, TraceId, ParentSpanId, flags de amostragem) e **`tracestate`** (dados do fornecedor) |
| **B3 Propagation** (mais antigo, do **Zipkin**) | Múltiplos: `X-B3-TraceId`, `X-B3-SpanId` |

- Com a **instrumentação automática**, é **automática** para HTTP, gRPC, RabbitMQ e Kafka.
- **Sem ela**: **traces quebrados**, só spans raiz desconectados em cada serviço.

Aparece em: [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]]
