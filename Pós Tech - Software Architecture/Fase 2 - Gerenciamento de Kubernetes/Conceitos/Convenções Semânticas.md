---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Semantic Conventions, Convenções semânticas do OpenTelemetry]
---

# Convenções Semânticas

Um conjunto de **nomes padronizados** do OpenTelemetry para **atributos e instrumentos**, que padroniza a busca e a visualização entre ferramentas e, segundo a aula 3, garante que **as métricas** geradas por diferentes bibliotecas sejam **consistentes e interoperáveis**.

- **Exemplos**: atributos `http.method`, `http.status_code`, `db.system` (traces); histograma **`http.server.duration`** para a duração de requisições de servidor HTTP (métricas).
- **Por que importam** (aula 5): se um serviço usa `http.status_code` e outro `response_code`, perdem-se as **consultas unificadas** e os **dashboards consistentes**.
- **Ação**: a equipe deve conhecer as convenções dos recursos usados (HTTP, banco, mensageria), na instrumentação **automática e manual**. Isso cria uma **linguagem comum** de telemetria na organização.

Aparece em: [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]], [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]], [[OTEL 05 - Boas práticas e desafios]]
