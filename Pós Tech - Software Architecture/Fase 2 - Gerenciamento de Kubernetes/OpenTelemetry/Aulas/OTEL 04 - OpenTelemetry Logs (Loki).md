---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, aula]
disciplina: OpenTelemetry
aula: 4
fonte: "OpenTelemetry/Aula 04 - OpenTelemetry Logs (Loki).pdf"
---

# OTEL 04 - OpenTelemetry Logs (Loki)

← [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]] · [[OpenTelemetry]] · Próxima → [[OTEL 05 - Boas práticas e desafios]]

> [!summary] Em uma frase
> Os **logs** são o terceiro pilar. A solução é o **[[Logs Estruturados|logging estruturado]]** (JSON), e o OTel permite injetar o **TraceId e o SpanId**, que **correlacionam os três pilares**. O **[[Grafana Loki]]** agrega os logs com a filosofia **"indexe os metadados, não os dados"**.

## Hands On
Gerar logs em **JSON**, enriquecidos automaticamente com o **ID do trace**. Adicionar o **Grafana Loki** e configurar o **Grafana** para criar um **link direto de qualquer linha de log para o trace** correspondente no **Jaeger**. Segundo o resumo, a pipeline de logs usa o **OTel Collector e o Loki**, as consultas são em **LogQL** e a ligação log → trace usa os **"Derived Fields"** do Grafana.

## O papel dos logs
- **Registros de eventos discretos** num ponto específico do tempo. Por décadas, a principal ferramenta de depuração ("deixa eu ver os logs"). Dão o **contexto granular** que traces e métricas nem sempre capturam.
- **Na era da observabilidade**: não são mais arquivos de texto isolados, mas um **fluxo de eventos estruturados**, pesquisável e **correlacionado** com os outros pilares.

| Papel | Exemplo do PDF |
|---|---|
| **Contexto detalhado** | O span diz que a operação levou 500 ms; o log diz por quê: "Timeout connecting to external API X", com stack trace |
| **Eventos inesperados** | Métricas e traces monitoram o esperado; logs capturam o **inesperado** (erros, exceções, comportamentos anômalos) |
| **Auditoria e segurança** | **Frequentemente** a fonte primária para **trilhas de auditoria**: quem fez o quê e quando |

- **Desafio em sistemas distribuídos**: dezenas ou centenas de serviços geram um volume massivo e disperso. É preciso **coletar de forma padronizada** e **agregar num sistema central**.

## Não estruturados × estruturados
- **Não estruturado**: `INFO: 2024-05-25 11:30:05 - Payment processed for user 123 in 150ms. OrderID: abc-456.` Legível para humanos, **terrível para máquinas**: buscar os pagamentos de um usuário exige **regex**, que é lento, frágil e caro.
- **Estruturado**: escrito em formato de máquina, como **JSON** (Figura 1 do PDF).
  - **Pesquisa eficiente**: consultar por campos (ex.: `user_id="123"` ou `duration_ms > 100`).
  - **Análise de dados**: os logs viram fonte para métricas e visualizações.
  - **Consistência**: todos os serviços registram de forma uniforme.
- O OpenTelemetry **formaliza o logging estruturado como padrão** para a coleta de logs.

## O LogRecord do OpenTelemetry
O OTel define um **modelo de dados de log**: um log de uma aplicação Java tem a mesma estrutura de um de Python, e back-ends como o Loki os processam de forma unificada.

| # | Campo | O que é |
|---|---|---|
| 1 | **Timestamp** | Quando o evento **ocorreu** |
| 2 | **ObservedTimestamp** | Quando o log foi **recebido pelo coletor**. A diferença para o Timestamp pode indicar **latência no pipeline** |
| 3 | **SeverityText** | Rótulo textual (INFO, WARN, ERROR) |
| 4 | **SeverityNumber** | Valor numérico, para filtrar (ex.: **INFO=9, ERROR=17**) |
| 5 | **Body** | O conteúdo principal: uma string ou uma estrutura (JSON) |
| 6 | **Attributes** | Pares chave-valor: os campos do log estruturado (`user_id`, `order_id`) |
| 7 | **Resource attributes** | Descrevem **quem produziu** o log (ex.: `service.name="payment-service"`, `k8s.pod.name="payment-7b..."`) |
| 8 | **TraceId e SpanId** | **O campo mais importante para a correlação**. O OTel pode injetá-los **automaticamente**, do trace ativo no momento do log |

## O poder da correlação
Com TraceId e SpanId em cada log, cria-se um **vínculo direto** entre os três pilares:
- **Trace → logs**: num trace lento no Jaeger, pegar o TraceId e o SpanId e, **com um clique**, ver os logs gerados durante aquele span.
- **Log → trace**: um log de erro no Loki tem o TraceId, então dá para saltar para o **trace completo** no Jaeger.
- **Métrica → logs → traces**: num pico de erros no Grafana, usar o intervalo de tempo para filtrar logs com `level="ERROR"` e depois analisar os traces.

> [!note] O terceiro caso aparece entre os benefícios do TraceId e do SpanId, mas o mecanismo descrito nele é o **intervalo de tempo** do pico. O texto também alterna entre `level="ERROR"` e `level="error"`.

Navegar entre os tipos de telemetria é o que define uma plataforma **verdadeiramente integrada** e é **o principal benefício** de usar o OpenTelemetry para os três sinais.

## Grafana Loki
- Sistema de **agregação de logs de código aberto**, da **Grafana Labs**, **inspirado no Prometheus**. Projetado para ser **econômico** e integrar com o ecossistema nativo da nuvem.
- **Filosofia**: **"Indexe os metadados, não os dados"**.

| | Elasticsearch (tradicional) | Loki |
|---|---|---|
| O que indexa | **Texto completo**: cada palavra e valor de cada linha | Só um **pequeno conjunto de labels** (os mesmos metadados do Prometheus), não o corpo |
| Vantagem | Pesquisas **muito rápidas e flexíveis** sobre o conteúdo | Índice **ordens de magnitude menor**; **eficiente em custo e operação** |
| Desvantagem | Indexar consome muita CPU, memória e **disco**; o índice pode custar **mais que os próprios logs**, o que encarece a operação em grande escala | Pode ser **mais lento** em consultas de texto completo muito amplas |

- **Fluxo de log**: um conjunto de logs com **exatamente os mesmos labels**. Ex.: `{job="payment-service", pod="payment-7b...", namespace="prod"}`.
- Os **logs brutos** são **comprimidos** e guardados em **chunks** num **armazenamento de objetos barato** (Amazon S3, Google Cloud Storage).

**Busca em duas etapas**
1. **Filtragem pelo índice**: um **seletor de labels** (ex.: `{job="payment-service", level="error"}`) encontra os fluxos. É **muito rápida**.
2. **Força bruta (grep)**: o Loki busca os chunks relevantes e filtra o conteúdo descomprimido (ex.: `|= "user_id=123"`).

> [!tip] A regra do Loki
> Use **labels para os filtros mais comuns** e o **filtro de conteúdo** para investigações mais específicas.

## Referências
Grafana: Grafana Loki Documentation · How to use LogQL range aggregations in Loki · OpenTelemetry: Logs
