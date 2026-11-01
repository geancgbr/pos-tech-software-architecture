---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Loki, LogQL]
---

# Grafana Loki

Sistema de **agregação de logs de código aberto**, da **Grafana Labs**, **inspirado no Prometheus**, projetado para ser **econômico**. A filosofia é **"Indexe os metadados, não os dados"**.

| | Elasticsearch | Loki |
|---|---|---|
| Indexa | **Texto completo** de cada log | Só um **pequeno conjunto de labels** |
| Prós | Pesquisas muito rápidas e flexíveis | Índice **ordens de magnitude menor**; barato de operar |
| Contras | Muita CPU, memória e disco; o índice pode custar mais que os logs | Mais lento em consultas de texto completo muito amplas |

- **Fluxo de log**: logs com **exatamente os mesmos labels** (ex.: `{job="payment-service", pod="payment-7b...", namespace="prod"}`).
- **Armazenamento**: os logs brutos são **comprimidos** em **chunks** num armazenamento de objetos barato (**Amazon S3, Google Cloud Storage**).
- **Busca**: (1) **seletor de labels** no índice, muito rápido; (2) **força bruta (grep)** no conteúdo (ex.: `|= "user_id=123"`).
- **Regra**: labels para os filtros mais comuns, filtro de conteúdo para investigações específicas. **Cardinalidade**: labels para infraestrutura (cluster, namespace, pod, service) e severidade; `user_id` e `trace_id` **no corpo** ([[Cardinalidade]]).
- **Segundo o resumo da aula 4**: consultas em **LogQL** no Grafana, e **"Derived Fields"** para ir de um log ao trace no [[Jaeger]].

## Na disciplina Monitoramento e Acesso (Fase 3)
- Projeto **inspirado no Prometheus**, mas **com foco em logs** (o Prometheus coleta métricas). **Open source**, como o Grafana.
- Segundo o PDF, **precisa estar no mesmo servidor do Grafana**, por ser **uma extensão da ferramenta**.
- **Instalação no Ubuntu**: `apt-get install loki promtail -y`. Configuração em `/etc/loki/loki.yml`, com o serviço na **porta 3100**, onde o [[Promtail]] envia os logs.
- **No Grafana**: data source Loki com a URL `http://localhost:3100`, e queries por **labels** em **Label Filters** → **Run Query**. → [[MON 03 - Prometheus e Grafana]]

Aparece em: [[OTEL 04 - OpenTelemetry Logs (Loki)]], [[OTEL 05 - Boas práticas e desafios]], [[MON 03 - Prometheus e Grafana]]
