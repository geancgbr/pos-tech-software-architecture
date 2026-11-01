---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Trace, Traces, Span, Spans, Tracing, Tracing distribuído, TraceId, SpanId, ParentSpanId, Span Kind, Root span]
---

# Traces e Spans

- **Trace**: a **jornada completa de uma única requisição** pelo sistema, "a história completa de uma transação". É um **conjunto de spans**.
- **Span**: uma **única unidade de trabalho** (chamada de API, consulta ao banco, renderização de template). Cada serviço tocado gera **pelo menos um span**.
- **Pai e filho**: os spans formam uma **árvore**. O primeiro é o **span raiz**; quando **o serviço desse span raiz** chama outro serviço, nasce um **span filho**, e o original é o **span pai**.

**Campos de um span**: **nome da operação** (legível e de alta cardinalidade) · **timestamps de início e fim** · **TraceId** (único global, compartilhado no trace) · **SpanId** · **ParentSpanId** (o raiz não tem) · **atributos** (chave-valor, com **[[Convenções Semânticas]]**) · **eventos** (como uma linha de log anexada) · **status** (**Unset** padrão, **Ok**, **Error**) · **Span Kind** (**SERVER**, **CLIENT**, **PRODUCER/CONSUMER**, **INTERNAL** padrão).

- **Atributos × eventos**: atributos descrevem a operação inteira; eventos marcam **pontos no tempo**.
- **Por que tracing**: sem ele, depurar latência em microsserviços é "resolver um mistério sem uma linha do tempo". O tracing mostra a **causalidade e o tempo** entre os serviços.
- Como os IDs viajam entre serviços: [[Propagação de Contexto]]. Back-end: [[Jaeger]].
- **Cardinalidade**: traces são **projetados para alta cardinalidade**; `user_id` pode ir nos spans ([[Cardinalidade]]).

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]]
