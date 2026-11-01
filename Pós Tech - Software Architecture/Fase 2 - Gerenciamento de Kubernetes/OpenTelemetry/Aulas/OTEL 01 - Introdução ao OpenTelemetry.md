---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, aula]
disciplina: OpenTelemetry
aula: 1
fonte: "OpenTelemetry/Aula 01 - Introdução ao OpenTelemetry.pdf"
---

# OTEL 01 - Introdução ao OpenTelemetry

[[OpenTelemetry]] · Próxima → [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]]

> [!summary] Em uma frase
> **Monitoramento** diz **se** algo está errado; **observabilidade** ajuda a descobrir **por que**. A observabilidade se apoia em **[[Três Pilares da Observabilidade (Logs, Métricas e Traces)|três pilares]]** (logs, métricas e traces). O **OpenTelemetry** (projeto da **CNCF**) é um **padrão aberto e um conjunto de ferramentas** para instrumentar, gerar, coletar e exportar telemetria, o que evita o **[[Vendor Lock-in|vendor lock-in]]**.

## Hands On
Uma aplicação web simples em **Python**, instrumentada **automaticamente** com as bibliotecas do OpenTelemetry e executada com **Docker**, com os **traces exibidos no console**. Segundo o resumo da aula, a aplicação é **Flask**.

## Monitoramento × observabilidade
| | Monitoramento | Observabilidade |
|---|---|---|
| Definição | Observar e coletar **dados pré-definidos** para verificar a saúde do sistema | Entender o **estado interno** de um sistema complexo só pelos **outputs externos** (telemetria) |
| Responde | **Se** algo está errado | **Por que** algo está errado, mesmo num problema nunca previsto |
| Analogia do carro | O **painel**, com luzes para problemas conhecidos (temperatura, óleo) | Um **scanner de diagnóstico** completo para o mecânico investigar a causa |
| Abordagem | **Reativa**, baseada em **"incógnitas conhecidas"** (known unknowns) | **Investigativa**, baseada em **"incógnitas desconhecidas"** (unknown unknowns) |
| Como | Você define o que observar (CPU, taxa de erros 5xx) e cria dashboards e alertas | Explorar os dados de telemetria para responder perguntas |

- **A observabilidade não substitui o monitoramento; ela o aprimora.** Exemplos de perguntas: "Por que os uploads estão lentos só para usuários no Brasil?", "Qual consulta ao banco causa lentidão na finalização da compra?", "Essa nova feature impactou o tempo de resposta de outros serviços?". Ver a Figura 1 do PDF.

## Os três pilares da observabilidade
| Pilar | O que é | Quando usar | Exemplo |
|---|---|---|---|
| **Logs** | Registro de um **evento discreto** num ponto específico do tempo. A forma **mais antiga e granular** de telemetria | Depuração detalhada, **análise forense**, fluxo de eventos num único componente | Não estruturado (ruim): `23/05/2024 20:30:00 ERROR: Falha de autenticação para o usuário ana.` Estruturado (bom): JSON com `timestamp`, `level`, `message`, `user_id`, `source_ip` |
| **Métricas** | **Agregação numérica** medida ao longo do tempo. **Leves e eficientes** para armazenar | Saúde geral, **tendências**, dashboards e **alertas** | `http_requests_total{method="POST", path="/api/payment", status="500"}`: um contador que incrementa a cada falha no endpoint de pagamento |
| **Traces** | A **jornada completa de uma requisição** por diferentes serviços. Um trace é uma **coleção de spans** | **Latência de ponta a ponta**, **gargalos**, dependências entre microsserviços | (o PDF não dá exemplo) |

- **Logs estruturados** (como JSON) são mais poderosos: podem ser **pesquisados, filtrados e agregados**.
- **Outros tipos de métrica**: **Gauges** (valor que sobe ou desce, como usuários ativos) e **Histograms** (distribuição estatística, como latências).
- **Span**: uma **única unidade de trabalho** (chamada de API, consulta ao banco). Tem um **identificador**, o **ID do trace** ao qual pertence, um **nome**, **timestamps de início e fim** e **metadados (atributos)**.

## O problema: vendor lock-in
Antes do OpenTelemetry: a empresa instrumenta todos os microsserviços com o **agente e a API proprietária** do Fornecedor A. Um ano depois, o Fornecedor B lança algo melhor e mais barato. Para migrar, é preciso **remover toda a instrumentação** e **reescrever** com a API do B, em dezenas ou centenas de serviços: **caro, demorado e arriscado**. Isso é o **vendor lock-in**.

## A solução: uma única especificação
- O **OpenTelemetry**, projeto da **Cloud Native Computing Foundation (CNCF)**, fornece um **padrão unificado**.
- **Ponto-chave**: o OpenTelemetry **não é uma plataforma de análise**. É um **padrão aberto e um conjunto de ferramentas** para **instrumentar, gerar, coletar e exportar** telemetria.
- Você instrumenta **uma vez** com a API do OTel e configura um **exportador** para qualquer back-end compatível. **Trocar de fornecedor vira uma mudança de configuração, não uma reescrita de código.**

## Arquitetura do OpenTelemetry
| Componente | O que é |
|---|---|
| **API** | Interfaces **agnósticas de implementação** que o código usa para gerar telemetria (ex.: `tracer.start_span()`) |
| **SDK** | A **implementação concreta da API** para uma linguagem (Python, Java...). Gerencia o **ciclo de vida dos spans**, a **amostragem (sampling)** e o processamento |
| **[[OpenTelemetry Collector\|Collector]]** | Um **serviço de proxy (agente)**, junto da aplicação ou num host separado. **Recebe** telemetria de várias fontes, pode **processá-la** (adicionar atributos, filtrar dados sensíveis) e **exportá-la** para um ou mais back-ends |
| **Exporters** | Módulos no SDK ou no Collector que **traduzem** os dados do OTel para o formato de um back-end (**Jaeger, Prometheus, Loki, Datadog**...) |

- Usar o **Collector** é **boa prática em produção**: desacopla as aplicações dos back-ends e centraliza a configuração de exportação.
- O formato nativo do OTel é o **OTLP (OpenTelemetry Protocol)**.
- Ver a Figura 2 do PDF (OpenTelemetry Architecture).

> [!note] Limite do console
> A saída no console é ótima para depuração e aprendizado, mas **impraticável** em sistemas reais: é impossível correlacionar e visualizar milhares de linhas de JSON.

> [!note] O resumo da aula fala em "componentes (API e SDK)", mas o corpo lista quatro: API, SDK, Collector e Exporters.

## Mercado, cases e tendências
O PDF recomenda o blog do OpenTelemetry e um post curto.

## Referências
OpenTelemetry: Instrumentation · OpenTelemetry Console Exporter · What is OpenTelemetry?
