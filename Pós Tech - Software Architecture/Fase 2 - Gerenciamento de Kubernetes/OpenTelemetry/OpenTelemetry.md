---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, indice]
disciplina: OpenTelemetry
fase: 2
aulas: 5
aliases: [OTel, OpenTelemetry (OTel)]
---

# OpenTelemetry

[[Fase 2 - Gerenciamento de Kubernetes]] · Revisão → [[Revisão - OpenTelemetry]]

> [!summary] O que é o OpenTelemetry, segundo as aulas
> Um projeto da **CNCF** que fornece um **padrão aberto e um conjunto de ferramentas** para **instrumentar, gerar, coletar e exportar** dados de telemetria. **Não é uma plataforma de análise**: você instrumenta uma vez com a API do OTel e exporta para **qualquer back-end compatível**, evitando o [[Vendor Lock-in]].

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[OTEL 01 - Introdução ao OpenTelemetry]] | [[Disponibilidade e Observabilidade\|Monitoramento × observabilidade]], [[Três Pilares da Observabilidade (Logs, Métricas e Traces)]], [[Vendor Lock-in]], [[OpenTelemetry Collector]] |
| 2 | [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]] | [[Jaeger]], [[Traces e Spans]], [[Propagação de Contexto]] |
| 3 | [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]] | [[Instrumentos de Métricas do OpenTelemetry]], [[Prometheus]], [[Grafana]] |
| 4 | [[OTEL 04 - OpenTelemetry Logs (Loki)]] | [[Logs Estruturados]], [[Grafana Loki]] |
| 5 | [[OTEL 05 - Boas práticas e desafios]] | [[Convenções Semânticas]], [[Cardinalidade]], [[Amostragem (Sampling)]], [[Tendências da Observabilidade (eBPF, Profiling e AIOps)]] |

## A arquitetura
| Componente | O que é |
|---|---|
| **API** | Interfaces **agnósticas de implementação** usadas pelo código (ex.: `tracer.start_span()`) |
| **SDK** | A **implementação concreta** da API por linguagem; gerencia o ciclo de vida dos spans, a **amostragem** e o processamento |
| **[[OpenTelemetry Collector\|Collector]]** | **Proxy (agente)** que recebe, **pode processar** e exporta telemetria. Boa prática em produção |
| **Exporters** | Traduzem os dados do OTel para o formato de cada back-end (Jaeger, Prometheus, Loki, Datadog) |

Formato nativo: **OTLP** (OpenTelemetry Protocol).

## Os pilares e seus back-ends na disciplina
| Pilar | Back-end | Visualização | Linguagem de consulta |
|---|---|---|---|
| Traces | [[Jaeger]] (storage: mais comuns, Elasticsearch e Cassandra) | Jaeger UI | (o PDF não informa) |
| Métricas | [[Prometheus]] (pull, TSDB) | [[Grafana]] | **PromQL** |
| Logs | [[Grafana Loki]] (índice só de labels) | [[Grafana]] | **LogQL** |

A tabela é só um mapa de navegação, montado a partir das aulas 2 a 4. O que liga tudo é o **TraceId** ([[Logs Estruturados]]).

## O ambiente do Hands On
Uma aplicação **Python (Flask)** instrumentada automaticamente e executada com **Docker** (aula 1). Na aula 2, o **OTel Collector** e o **Jaeger** entram no ambiente com **Docker Compose**. O **Prometheus** (aula 3) e o **Loki** (aula 4) são adicionados ao ambiente, e o **Grafana** é conectado ao Prometheus (aula 3).

## Ligações com outras disciplinas
- **Kubernetes**: o Prometheus é apontado como **padrão de fato** para métricas em ambientes Kubernetes e se integra a mecanismos de descoberta de serviços, **como a API do Kubernetes** (aula 3). O Collector pode rodar como **DaemonSet** (aula 5). A parte 2 de Kubernetes também trata de [[EFK (Elasticsearch, Fluentd e Kibana)|EFK]], [[Prometheus]] e [[Grafana]] ([[K8S2 09 - Monitoramento e logging do EKS]]).
- **Dockerização**: o ambiente do Hands On usa [[Docker]] e [[Docker Compose]].
- **Arquitetura de Software (Fase 1)**: observabilidade em [[Disponibilidade e Observabilidade]].

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
O OpenTelemetry aparece como projeto da CNCF com APIs, bibliotecas e agentes para coletar **traces e métricas**, combinando **OpenTracing** e **OpenCensus**, com boas práticas de **dados contextuais**, **nomenclatura** e **amostragem** (ex.: 50%). Ver [[MS2 06 - Realizando o deploy de microsserviços, parte 2]].

## Material
PDFs em `~/Desktop/OpenTelemetry/` ("Aula 01 - Introdução ao OpenTelemetry.pdf" a "Aula 05 - Boas práticas e desafios .pdf").
