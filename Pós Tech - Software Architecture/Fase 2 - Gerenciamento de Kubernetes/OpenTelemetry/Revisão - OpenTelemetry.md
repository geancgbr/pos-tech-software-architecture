---
tags: [pos-tech/fase-2, opentelemetry, revisao]
disciplina: OpenTelemetry
---

# Revisão - OpenTelemetry

[[OpenTelemetry]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- Monitoramento × observabilidade?
> Monitoramento coleta dados pré-definidos e diz **se** algo está errado: é reativo, de "incógnitas conhecidas". Observabilidade entende o estado interno pelos outputs externos e ajuda a descobrir **por que**: é investigativa, de "incógnitas desconhecidas". → [[OTEL 01 - Introdução ao OpenTelemetry]]

> [!question]- Qual a analogia do carro?
> O monitoramento é o painel, com luzes para problemas conhecidos. A observabilidade é um scanner de diagnóstico completo, que permite investigar a causa.

> [!question]- A observabilidade substitui o monitoramento?
> Não: ela o aprimora.

> [!question]- Quais são os três pilares, e quando usar cada um?
> Logs (depuração detalhada, análise forense), métricas (saúde geral, tendências, dashboards e alertas) e traces (latência de ponta a ponta, gargalos, dependências entre microsserviços). → [[Três Pilares da Observabilidade (Logs, Métricas e Traces)]]

> [!question]- Por que logs estruturados são melhores?
> Podem ser facilmente pesquisados, filtrados e agregados por ferramentas de análise.

> [!question]- O que é vendor lock-in, e como o OTel resolve?
> O cenário em que instrumentar com o agente e a API proprietária de um fornecedor obriga, para migrar, a remover e reescrever toda a instrumentação: caro, demorado e arriscado. O OTel é um padrão unificado: instrumenta-se uma vez e troca-se o exportador por configuração. → [[Vendor Lock-in]]

> [!question]- O OpenTelemetry é uma plataforma de análise?
> Não. É um padrão aberto e um conjunto de ferramentas para instrumentar, gerar, coletar e exportar telemetria.

> [!question]- Quais os componentes da arquitetura do OTel?
> API (interfaces agnósticas), SDK (implementação por linguagem, com ciclo de vida dos spans e amostragem), Collector (proxy que recebe, pode processar e exporta) e Exporters (traduzem para cada back-end). O formato nativo é o OTLP. → [[OpenTelemetry#A arquitetura]]

## Aula 2 - Tracing (Jaeger)
> [!question]- O que é o Jaeger, e quem o criou?
> Um projeto de código aberto graduado pela CNCF, criado na Uber, para armazenar, encontrar e visualizar traces. → [[Jaeger]]

> [!question]- Quais são os componentes do Jaeger?
> Jaeger Client (obsoleto), Jaeger Collector, Storage Back-end (as opções mais comuns são Elasticsearch e Cassandra, porque ele não tem armazenamento próprio), Jaeger Query e Jaeger UI.

> [!question]- Qual o fluxo de um span da aplicação até a Jaeger UI?
> SDK OTel → OTLP → OTel Collector (pode processar) → jaeger exporter → Jaeger Collector → storage → Jaeger UI (via Jaeger Query).

> [!question]- Trace × span × relação pai-filho?
> O trace é a jornada de uma requisição, um conjunto de spans. O span é uma unidade de trabalho. Os spans formam uma árvore: o span raiz e, quando o serviço desse span raiz chama outro serviço, um span filho; o original é o span pai. → [[Traces e Spans]]

> [!question]- Quais os campos de um span?
> Nome da operação, timestamps de início e fim, TraceId/SpanId/ParentSpanId, atributos, eventos, status (Unset, Ok, Error) e Span Kind.

> [!question]- Atributos × eventos?
> Atributos descrevem a operação como um todo; eventos marcam pontos específicos no tempo, como uma linha de log anexada ao span.

> [!question]- Quais são os Span Kinds?
> SERVER (requisição recebida), CLIENT (requisição feita), PRODUCER/CONSUMER (mensageria) e INTERNAL (não cruza fronteiras de processo; é o padrão).

> [!question]- Como funciona a propagação de contexto?
> Injeção do contexto nos metadados da requisição (em HTTP, cabeçalhos) pelo cliente, extração pelo servidor e criação do span filho com o TraceId e o ParentSpanId recebidos. → [[Propagação de Contexto]]

> [!question]- W3C Trace Context × B3?
> W3C: o padrão oficial e recomendado, com `traceparent` e `tracestate`. B3: mais antigo, do Zipkin, com vários cabeçalhos (`X-B3-TraceId`, `X-B3-SpanId`).

> [!question]- O que acontece sem propagação de contexto?
> Traces quebrados: só spans raiz desconectados em cada serviço.

## Aula 3 - Metrics (Prometheus)
> [!question]- Por que as métricas são essenciais?
> Visão macroscópica, eficiência de armazenamento, base para alertas e SLOs, e correlação com traces e logs. → [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]]

> [!question]- Quais os seis instrumentos de métricas do OTel?
> Síncronos: Counter, UpDownCounter e Histogram. Assíncronos: Asynchronous Counter, Asynchronous UpDownCounter e Asynchronous Gauge. → [[Instrumentos de Métricas do OpenTelemetry]]

> [!question]- Instrumento síncrono × assíncrono?
> Síncrono: chamado em linha com o código, no momento do evento. Assíncrono: um callback que o SDK chama periodicamente para ler o valor atual.

> [!question]- Por que usar Histogram para latência?
> Agrupa as medições em buckets e permite calcular média e percentis (p95, p99), mais representativos da experiência do usuário do que uma simples média.

> [!question]- Modelo push × pull?
> Push: a aplicação envia as métricas. Pull (Prometheus): a aplicação expõe `/metrics` e o servidor raspa (scrape) em intervalos regulares. → [[Prometheus]]

> [!question]- Quais as vantagens do modelo pull?
> Controle centralizado, resiliência, descoberta de serviços (como a API do Kubernetes) e simplicidade do alvo.

> [!question]- Quais as peças da arquitetura do Prometheus?
> Servidor (Scraping Engine, TSDB, PromQL Engine, API HTTP), Alertmanager (agrupa, desduplica e roteia alertas) e Exporters (convertem métricas de sistemas que não usam o formato Prometheus).

> [!question]- Quais as duas abordagens principais para integrar OTel e Prometheus?
> 1) Prometheus Exporter no SDK: a aplicação expõe `/metrics` (simples, mas exige porta exposta e acopla a aplicação). 2) OTel Collector como ponte: a aplicação faz push OTLP e o Prometheus raspa o Collector (desacoplamento, gestão e processamento centralizados).

## Aula 4 - Logs (Loki)
> [!question]- Quais papéis os logs têm na observabilidade?
> Contexto detalhado (o porquê de um span lento), eventos inesperados e auditoria e segurança. → [[OTEL 04 - OpenTelemetry Logs (Loki)]]

> [!question]- Quais os campos de um LogRecord?
> Timestamp, ObservedTimestamp, SeverityText, SeverityNumber, Body, Attributes, Resource attributes e TraceId/SpanId. → [[Logs Estruturados]]

> [!question]- Qual campo é o mais importante para a correlação, e por quê?
> O TraceId e o SpanId: permitem ir do trace aos logs do span, do log ao trace completo e, de um pico de métrica, usar o intervalo de tempo para filtrar os logs e, a partir deles, analisar os traces.

> [!question]- Qual a filosofia do Loki, e como ela difere do Elasticsearch?
> "Indexe os metadados, não os dados": indexa só os labels, não o corpo. O Elasticsearch indexa o texto completo (rápido e flexível, mas caro). → [[Grafana Loki]]

> [!question]- Como funciona uma busca no Loki?
> Primeiro, a filtragem pelo índice com um seletor de labels; depois, uma busca por força bruta (grep) no conteúdo dos chunks.

## Aula 5 - Boas práticas e desafios
> [!question]- Qual a narrativa da depuração moderna?
> Métrica (o alerta: **o que** está errado) → trace (o contexto: **onde**) → log (a causa raiz: **por que**), com o TraceId como fio condutor. → [[OTEL 05 - Boas práticas e desafios]]

> [!question]- Quais as quatro boas práticas fundamentais?
> Usar as convenções semânticas, combinar instrumentação automática (a base) e manual (o contexto de negócio), usar o OTel Collector como intermediário e gerenciar a cardinalidade.

> [!question]- O que é cardinalidade, e por que ela é um problema?
> O número de valores únicos de um atributo. Cada combinação de labels cria uma série temporal (Prometheus) ou um fluxo (Loki); atributos como `user_id` como labels causam uma explosão de cardinalidade. → [[Cardinalidade]]

> [!question]- Onde pode ir `user_id`?
> Nos spans (traces são projetados para alta cardinalidade) e no corpo do log. Nunca como label no Prometheus; no Loki, manter no corpo da mensagem.

> [!question]- Amostragem head-based × tail-based?
> Head-based: por proporção, no SDK, para reduzir a carga na aplicação. Tail-based: políticas inteligentes no Coletor, para reter os traces importantes, como 100% dos erros. → [[Amostragem (Sampling)]]

> [!question]- Quais os desafios comuns na adoção do OTel?
> Overhead de performance, volume de dados e custo, curva de aprendizagem, e instrumentação de código legado e de terceiros.

> [!question]- Como reduzir o custo da observabilidade?
> Amostragem agressiva dos traces bem-sucedidos (muitas vezes 1% a 5% basta, mantendo 100% dos com erro), políticas de retenção diferentes e filtragem no Coletor (logs de DEBUG, health checks).

> [!question]- O que é eBPF, e por que importa?
> Tecnologia do kernel Linux que roda programas em sandbox, permitindo coletar telemetria sem instrumentar o código. → [[Tendências da Observabilidade (eBPF, Profiling e AIOps)]]

> [!question]- Qual é o quarto pilar?
> O continuous profiling: CPU e memória até a linha de código, visualizado em flame graphs.

> [!question]- O que muda na cultura de observabilidade?
> A responsabilidade é compartilhada: "You Build It, You Run It, You Own It", os devs instrumentam como parte do ciclo (como os testes unitários) e os dados servem a todos.

## Dúvidas em aberto
- Quem explica o "por quê"? A aula 3 diz que são os traces ("onde e por quê"); a aula 5 atribui o "por quê" ao log.
- Gauge: a aula 1 dá "usuários ativos" como exemplo; a aula 3 usa o UpDownCounter para "conexões ativas".
- Aula 3: o exemplo troca `http_requests_total` por `http.server.request_count`.
- Aula 4: no terceiro caso de correlação, o salto da métrica para os logs usa o intervalo de tempo, não o TraceId.
- Aula 1: o resumo fala em "componentes (API e SDK)", mas o corpo lista quatro componentes.

## Pontos fracos (o que errei)
