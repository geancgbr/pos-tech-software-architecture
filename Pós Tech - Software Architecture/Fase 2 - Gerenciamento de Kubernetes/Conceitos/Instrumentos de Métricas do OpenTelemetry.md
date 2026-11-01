---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Instrumentos de métricas, Counter, UpDownCounter, Histogram, Gauge, Asynchronous Gauge, Instrumento]
---

# Instrumentos de Métricas do OpenTelemetry

O **instrumento** é a ferramenta no código para **registrar medições**. A escolha define o **tipo de agregação** e a **semântica** da métrica. São seis, agrupados por **sincronicidade**:

| Síncronos (chamados no momento do evento) | Assíncronos (callback chamado periodicamente pelo SDK) |
|---|---|
| **Counter**: **só aumenta** (requisições, bytes). Agregação **Sum**; o Prometheus pode calcular a taxa com `rate()` | **Asynchronous Counter**: soma que só aumenta (tempo de CPU total do processo) |
| **UpDownCounter**: **sobe e desce** (conexões ativas, itens na fila). Sum positiva ou negativa, para ver o **valor atual** | **Asynchronous UpDownCounter**: sobe e desce (tamanho de um cache, `cache.size()`) |
| **Histogram**: **distribuições** (latências, payloads) em **buckets**. Permite **média e percentis (p95, p99)** | **Asynchronous Gauge**: valor que sobe e desce arbitrariamente, com medições **não somáveis** (uso atual de CPU ou memória, temperatura). "Um dos mais comuns" |

- **Atributos (labels ou dimensões)**: fatiar e filtrar (por `http.method`, `http.status_code`, `customer.tier`, `region`). Cuidado com a [[Cardinalidade]].
- **Convenções Semânticas**: a duração de requisição de servidor HTTP vai no histograma **`http.server.duration`** ([[Convenções Semânticas]]).
- **Na aula 1**: o exemplo é um contador (`http_requests_total`); "outros tipos" são **Gauges** (ex.: usuários ativos) e **Histograms**.

> [!note] A aula 1 dá o Gauge para "usuários ativos". A aula 3 usa o UpDownCounter para "conexões ativas" e só traz o Gauge na versão assíncrona, para medições não somáveis.

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]]
