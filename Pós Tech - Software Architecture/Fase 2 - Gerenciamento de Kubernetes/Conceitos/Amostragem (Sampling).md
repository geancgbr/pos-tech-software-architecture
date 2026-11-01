---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Amostragem, Sampling, Head-based sampling, Tail-based sampling, Head-based, Tail-based]
---

# Amostragem (Sampling)

Processar e exportar **só uma parte** dos traces, em vez de 100%. É **a principal ferramenta** para controlar o **overhead de tracing**. No OTel, a amostragem é gerenciada pelo **SDK** (aula 1) e também pode ser feita no **Collector** (aula 2).

| | Head-based | Tail-based |
|---|---|---|
| Onde | No **SDK** | No **Coletor** |
| Como | **Por proporção** | **Políticas inteligentes** |
| Para quê | Reduzir a carga na aplicação | Reter os traces importantes, como **100% dos erros**, sem sobrecarregar o back-end |

- **Combinar as duas**: head-based no SDK + tail-based no Coletor.
- **Contra o custo**: amostrar **pesadamente** os traces bem-sucedidos (muitas vezes **1% a 5%** basta para a análise de performance geral), mantendo **100% dos traces com erro**.
- O `traceparent` da [[Propagação de Contexto]] carrega **flags de amostragem**.

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]], [[OTEL 05 - Boas práticas e desafios]]
