---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, aula]
disciplina: OpenTelemetry
aula: 2
fonte: "OpenTelemetry/Aula 02 - OpenTelemetry Tracing (Jaeger).pdf"
---

# OTEL 02 - OpenTelemetry Tracing (Jaeger)

← [[OTEL 01 - Introdução ao OpenTelemetry]] · [[OpenTelemetry]] · Próxima → [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]]

> [!summary] Em uma frase
> Para sair do console, os traces vão para um back-end de visualização: o **[[Jaeger]]**. O **OTel Collector** funciona como agente central. O tracing segue a requisição **de ponta a ponta**, como uma **árvore de [[Traces e Spans|spans]]**, e a **[[Propagação de Contexto]]** liga os spans de serviços diferentes num mesmo trace.

## Hands On
Adicionar o **Jaeger** e o **OpenTelemetry Collector** ao ambiente com **Docker Compose**. O Collector recebe os dados da aplicação e os envia ao Jaeger. Depois, fazer requisições e explorar a interface, analisando a **jornada e a latência** de cada uma. Segundo o resumo, o Collector foi configurado com um pipeline de **recebimento, processamento e exportação**.

## O Jaeger
Projeto **de código aberto**, **graduado pela CNCF**, criado na **Uber** como seu sistema de **tracing distribuído**. Serve para **armazenar, encontrar e visualizar traces**. Pode ser implantado de diferentes maneiras, **desde** uma instância **"all-in-one"** (desenvolvimento local) **até** uma arquitetura escalável para produção.

| Componente | Papel |
|---|---|
| **Jaeger Client** (**obsoleto**) | As antigas bibliotecas de instrumentação do Jaeger. Hoje, o recomendado é o **SDK do OpenTelemetry** com um **exportador OTLP** |
| **Jaeger Collector** | **Recebe** os traces (via OTLP, por exemplo), **valida, indexa e armazena** num banco |
| **Storage Back-end** | O Jaeger **não tem armazenamento próprio**. Integra com bancos existentes, mais comumente **Elasticsearch** e **Cassandra** |
| **Jaeger Query** | Expõe uma **API** para buscar traces do storage |
| **Jaeger UI** | Interface web que usa o Jaeger Query para **pesquisar e visualizar** traces |

## O fluxo com OpenTelemetry e Jaeger
1. **Aplicação instrumentada** (SDK OTel) gera spans.
2. O SDK exporta os spans via **OTLP** para o **OTel Collector** (recomendado).
3. O Collector pode **processar** (amostragem, adição de atributos) e exporta com o **jaeger exporter**.
4. O **Jaeger Collector** recebe os spans.
5. Os spans vão para o **storage** (ex.: Elasticsearch).
6. A **Jaeger UI** usa o Jaeger Query para buscar e renderizar os traces.

Ver a Figura 1 do PDF (Jaeger Architecture).

## Por que tracing
- Segue a requisição por vários microsserviços **de ponta a ponta**, mostrando quais serviços foram tocados e a **relação de causalidade e tempo** entre eles.
- **Sem tracing**, depurar latência em microsserviços é "como tentar resolver um mistério sem uma linha do tempo". Você tem logs de cada serviço, mas não sabe como se conectam: o Serviço A demorou para chamar o B, ou o B demorou para responder? O tracing responde **de forma visual e definitiva**.

## Conceitos fundamentais
- **Trace**: a jornada completa de **uma única requisição**; um **conjunto de spans**, "a história completa de uma transação".
- **Span**: uma única unidade de trabalho. **Cada serviço tocado gera pelo menos um span.** Operações como uma chamada de banco, uma renderização de template ou uma chamada a API externa **podem ser** um span. Tem nome, hora de início, duração e metadados.
- **Relação pai-filho**: os spans formam uma **árvore**. O primeiro é o **span raiz** (root span). Quando **o serviço desse span raiz** chama outro serviço, nasce um **span filho** (child span), e o original é o **span pai** (parent span).
- O objetivo do **OpenTelemetry Tracing** é um padrão para **criar, propagar e coletar** spans, reconstruindo a história da requisição sem importar quantas fronteiras de processo, rede ou tecnologia ela cruze.

## O modelo de dados de um span
| # | Campo | O que é |
|---|---|---|
| 1 | **Nome da operação** | Legível e de **alta cardinalidade** (ex.: `HTTP GET /api/users`, `db.query`, `render_user_profile`) |
| 2 | **Timestamps de início e fim** | Para calcular a duração exata |
| 3 | **TraceId** / **SpanId** / **ParentSpanId** | TraceId: **único global**, compartilhado por todos os spans do trace. SpanId: único do span. ParentSpanId: o SpanId do pai, que estabelece a relação pai-filho (o **span raiz não tem**) |
| 4 | **Atributos** | Pares **chave-valor**: a principal forma de dar **contexto pesquisável** ("tags"). As **Convenções Semânticas** padronizam os nomes (ex.: `http.method`, `http.status_code`, `db.system`) |
| 5 | **Eventos** | Mensagem **com data e hora** sobre algo que aconteceu durante o span, como **uma linha de log anexada** (ex.: `Cache miss`, `User validation failed`) |
| 6 | **Status** | **Unset** (padrão), **Ok** ou **Error**, opcionalmente com mensagem. `Error` faz as ferramentas destacarem o ponto |
| 7 | **Span Kind** | A relação com um sistema remoto (tabela abaixo) |

- **Atributos × eventos**: os atributos descrevem **a operação como um todo**; os eventos marcam **pontos específicos no tempo** dentro dela.

| Span Kind | Representa |
|---|---|
| **SERVER** | Uma requisição **sendo recebida** (ex.: controlador de API) |
| **CLIENT** | Uma requisição **sendo feita** a um sistema remoto (chamada HTTP, consulta ao banco) |
| **PRODUCER / CONSUMER** | Produção e consumo de **mensagens** |
| **INTERNAL** | Operação que **não cruza fronteiras de processo** (**padrão**) |

## Propagação de contexto
Como o TraceId e o ParentSpanId viajam do Serviço A para o B? Pela **[[Propagação de Contexto|propagação de contexto]]**.
- O **contexto (Context)** é um objeto do OTel com o TraceId e o SpanId do span ativo. A propagação o **serializa**, envia pela rede (geralmente em **cabeçalhos**) e **desserializa** no receptor.
1. **Injeção** (cliente, Serviço A): o SDK "injeta" o contexto nos metadados da requisição. Para uma chamada HTTP, isso significa adicionar cabeçalhos.
2. **Extração** (servidor, Serviço B): o SDK "extrai" o contexto.
3. **Criação do span filho**: com o TraceId e o ParentSpanId de A, o B cria um span (SpanId próprio) ligado como filho.

| Padrão | Características |
|---|---|
| **W3C Trace Context** (**recomendado**) | Padrão oficial da W3C e recomendação do OpenTelemetry. **`traceparent`**: versão, TraceId, ParentSpanId e flags de amostragem. **`tracestate`**: informações específicas do fornecedor |
| **B3 Propagation** | Mais antigo, **originado no Zipkin**, ainda muito usado. Múltiplos cabeçalhos (`X-B3-TraceId`, `X-B3-SpanId`) |

- Com a **instrumentação automática**, a injeção e a extração para protocolos comuns (**HTTP, gRPC, RabbitMQ, Kafka**) são **automáticas**. Quem desenvolve raramente mexe nisso, mas precisa saber que acontece.
- **Sem propagação**: traces **quebrados**, uma coleção de spans raiz em cada serviço, sem conexão entre eles.

## Referências
GitHub: OTLP Exporter · Jaeger: Introduction · OpenTelemetry: OpenTelemetry Collector
