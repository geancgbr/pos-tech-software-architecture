---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, aula]
disciplina: OpenTelemetry
aula: 3
fonte: "OpenTelemetry/Aula 03 - OpenTelemetry Metrics (Prometheus).pdf"
---

# OTEL 03 - OpenTelemetry Metrics (Prometheus)

← [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]] · [[OpenTelemetry]] · Próxima → [[OTEL 04 - OpenTelemetry Logs (Loki)]]

> [!summary] Em uma frase
> As **métricas** são o segundo pilar: a **visão agregada e panorâmica** da saúde do sistema ao longo do tempo. O OpenTelemetry define **seis [[Instrumentos de Métricas do OpenTelemetry|instrumentos]]** (três síncronos e três assíncronos). O **[[Prometheus]]** armazena e consulta as métricas com um **modelo pull**, e há **duas abordagens principais** para integrá-lo ao OTel.

## Hands On
Configurar a aplicação e o Collector para exportar métricas, adicionar o **Prometheus** para coletá-las (**scrape**) e conectar o **Grafana** ao Prometheus num dashboard com os indicadores **RED**: **taxa de requisições, erros e duração**. Segundo o resumo, também foram escritas as primeiras queries em **PromQL**.

## Por que métricas
Se os traces contam a história detalhada de **uma** requisição, as métricas dão a **visão agregada** ao longo do tempo: **medições numéricas**, geralmente coletadas em **intervalos regulares**, para perguntas quantitativas.

| Motivo | O que o PDF diz |
|---|---|
| **Visão macroscópica** | Tendências, padrões e anomalias em larga escala. Um pico no tempo de resposta ou na taxa de erros aparece de imediato num gráfico |
| **Eficiência de armazenamento** | Guardam só **valores numéricos agregados**, não os detalhes de cada requisição. Ideais para **retenção de longo prazo** |
| **Alertas e SLOs** | Base dos alertas: **limiares (thresholds)** que disparam avisos (ex.: "Alertar se a taxa de erros do serviço de pagamentos for maior que 2% por mais de 5 minutos"). Fundamentais para os **SLOs** (Objetivos de Nível de Serviço) |
| **Correlação** | Sozinhas, podem não explicar a causa raiz. O dashboard mostra **o que** está errado (a latência subiu), e os traces mostram **onde e por quê** |

## O modelo de métricas do OpenTelemetry
- O ponto central é o **instrumento**: a ferramenta no código para **registrar medições**. A escolha define o **tipo de agregação** e a **semântica** da métrica.
- **Síncronos**: chamados **em linha com o código**, no momento do evento. **Assíncronos (observáveis)**: você registra um **callback** que o SDK chama **periodicamente** para obter o valor atual, o que é ideal para valores **já mantidos em algum lugar**.

| # | Instrumento | Tipo | O que mede | Exemplo | Agregação |
|---|---|---|---|---|---|
| 1 | **Counter** | Síncrono | Valor que **só aumenta** (monotônico): requisições, tarefas, bytes | `http.server.request_count.add(1)` | **Sum** desde o início. A ferramenta de visualização (como o Prometheus) **pode calcular** a taxa com `rate()` |
| 2 | **UpDownCounter** | Síncrono | Valor que **sobe ou desce**: conexões ativas, itens numa fila | `queue.items.add(1)` / `queue.items.add(-1)` | **Sum** positiva ou negativa: uma contagem "instantânea", útil para ver o **valor atual**, não para taxas |
| 3 | **Histogram** | Síncrono | **Distribuições** (latências, tamanhos de payload), agrupadas em **buckets** pré-definidos | `http.server.duration.record(125.5)` (ms) | Contagem total, soma total e contagem por bucket (ex.: 0-50 ms, 50-100 ms). Permite **média e percentis (p95, p99)**, mais representativos da experiência do usuário que a média |
| 4 | **Asynchronous Counter** | Assíncrono | Versão assíncrona do Counter (soma que só aumenta) | Tempo de CPU total de um processo, lido do SO a cada intervalo || (o PDF não informa) |
| 5 | **Asynchronous UpDownCounter** | Assíncrono | Versão assíncrona do UpDownCounter | Tamanho de um cache em memória (`cache.size()`) || (o PDF não informa) |
| 6 | **Asynchronous Gauge** | Assíncrono | Valor que sobe e desce **arbitrariamente**, com medições **não somáveis**. "Um dos instrumentos mais comuns" | Uso atual de CPU ou memória, temperatura de um sensor || (o PDF não informa) |

> [!note] Na aula, o Prometheus é chamado de "ferramenta de visualização" ao falar do `rate()`, mas na mesma aula a visualização é feita pelo Grafana.

- **Atributos (labels ou dimensões)**: pares chave-valor para **fatiar e filtrar**. Ex.: `http.server.request_count{http.method="GET", http.status_code="200"}`, `...="404"}`, `{http.method="POST", http.status_code="201"}`. Permitem analisar por método, status ou outra dimensão (como `customer.tier` ou `region`).
> [!note] O texto diz "em vez de ter uma única métrica `http_requests_total`", mas os exemplos logo abaixo usam `http.server.request_count`.

- **Convenções Semânticas**: nomes consistentes entre bibliotecas. Ex.: a duração de uma requisição de servidor HTTP deve ir no histograma **`http.server.duration`**.

## Prometheus
- Sistema de **monitoramento e alerta de código aberto**, **graduado pela CNCF**, criado na **SoundCloud**. Tornou-se o **padrão de fato** para métricas em ambientes **Kubernetes**.
- **O que o diferencia**: o **modelo pull**.

| | Modelo push | Modelo pull (Prometheus) |
|---|---|---|
| Quem age | A aplicação **envia** as métricas a um endpoint central | A aplicação (o **alvo**, target) **expõe** as métricas num endpoint HTTP (geralmente **`/metrics`**), e o servidor **"raspa" (scrape)** em intervalos regulares (ex.: a cada **15 s**) |

**Vantagens do pull**
- **Controle centralizado**: quais alvos e com que frequência fica tudo no servidor Prometheus.
- **Resiliência**: se o servidor ficar indisponível, as aplicações seguem normais; quando ele volta, continua raspando.
- **Descoberta de serviços**: integra nativamente com mecanismos como a **API do Kubernetes**, descobrindo novos contêineres e serviços automaticamente.
- **Simplicidade do alvo**: a aplicação só expõe um endpoint de texto, sem lógica de envio, retentativas ou endereço do back-end.

**Arquitetura**
| Peça | Papel |
|---|---|
| **Servidor Prometheus** | O núcleo: **Scraping Engine** (raspagem), **TSDB** (banco de séries temporais no disco local), **PromQL Engine** (consultas em **PromQL**) e **API HTTP** (para visualização, como o Grafana, e para o Alertmanager) |
| **Alertmanager** | Componente **separado** de alertas: recebe as regras do Prometheus, **agrupa, "desduplica" e roteia** notificações (Slack, e-mail, PagerDuty) |
| **Exporters** | Pequenos serviços ao lado de sistemas que **não expõem métricas no formato Prometheus** (bancos, hardware, mensageria): coletam e **convertem** para raspagem |

Ver a Figura 1 do PDF (Prometheus Architecture).

## Integrando OpenTelemetry com Prometheus
O OTel foi projetado principalmente em **push** (o SDK exporta); o Prometheus opera em **pull**. Há **duas abordagens principais** para conciliar:

| | Abordagem 1: Prometheus Exporter no SDK | Abordagem 2: OTel Collector como ponte |
|---|---|---|
| Como funciona | A **própria aplicação vira alvo**: em vez do exportador OTLP, configura-se o **Prometheus Exporter** no SDK, que sobe um **servidor HTTP** com `/metrics` e converte as métricas para o formato de texto do Prometheus quando raspado | A aplicação usa o **OTLP Exporter** e faz **push** ao Collector, a única configuração que ela conhece. O Collector habilita o **Prometheus Exporter** dele, que expõe `/metrics`, e o Prometheus raspa **o Collector**, não cada aplicação |
| Vantagens | **Simples** para começar; alinhada ao design do Prometheus | **Desacoplamento total** (para mandar também ao Datadog, basta um **datadog exporter** no Collector) · **gerenciamento centralizado** (o Prometheus só conhece os coletores) · **processamento central** (enriquecer, filtrar ou agregar para todos os serviços) |
| Desvantagens | **Segurança e rede**: expor uma porta HTTP em cada instância e dar acesso ao Prometheus. **Acoplamento**: a aplicação sabe que é monitorada pelo Prometheus; mudar para um back-end push (como o Datadog) exige mudar a configuração dela | — (o PDF não lista) |

- **Modo reverso**: o Collector pode usar um **Prometheus Receiver** para **raspar alvos existentes** e converter para **OTLP**, enviando a outros back-ends. Essa flexibilidade torna o **OTel Collector a peça central** de qualquer estratégia moderna de telemetria.

## Referências
Grafana: Technical Documentation · OpenTelemetry: Metrics · Prometheus: Overview
