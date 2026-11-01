---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Hystrix, Netflix Hystrix]
---

# Resilience4j

Biblioteca Java para resiliência **simples e declarativa**, criada por **Robert Winkler** como alternativa **leve e modular** ao **Netflix Hystrix**, descontinuado em **2018**; aproveita o **Java 8+** e funciona com ou sem **Spring Boot** ([[RES 03 - Resiliência na prática]]).

- Equivalentes: **Go** (Go-resiliency, Resilience), **Node.js** (opossum, p-retry), **.NET** (Polly).
- [[Circuit Breaker]] com **janela deslizante** por **contagem** ou por **tempo**, ambas com **Subtract-on-Evict**; parâmetros `slidingWindowType`, `slidingWindowSize`, `failureRateThreshold`, `waitDurationInOpenState`; `@CircuitBreaker(name, fallbackMethod)`.
- Nas videoaulas: **Retry**, **Bulkhead** e **Rate Limiter**.
- Já citado na aula 2 como implementação do Circuit Breaker, junto com o Hystrix ([[RES 02 - Padrões de resiliência]]).

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]]
