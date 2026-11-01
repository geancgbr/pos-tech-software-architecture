---
tags: [pos-tech/fase-3, monitoramento, datadog, alertas, conceito]
aliases: [Monitors, Monitor, Datadog Monitors, Fadiga de alerta, Alert Fatigue, MTTD, MTTR]
---

# Monitors do Datadog

A funcionalidade **"Monitors"** é **o coração do alerting** no [[Datadog]]: uma regra (ou conjunto de regras) que, atendida, **dispara um alerta** ([[MAV 05 - Criando alertas com DD]]).

- **Por que alertar de forma proativa**: menor **MTTD** (Mean Time To Detect) e **MTTR** (Mean Time To Resolve), experiência do usuário, eficiência operacional e prevenção de perdas.
- **Anatomia**: **método de detecção** (Threshold, Anomaly, Forecast, Outlier) · **métrica/query** (com tags) · **condições** (Alert/Warning, janela de avaliação, No Data, auto-resolve) · **notificação** (variáveis de template como `{{host.name}}`, `{{value}}`, `{{threshold}}`; @-mentions) · **renotificação** · **agrupamento** (multi-alert) · **permissões**.
- **Tipos**: Metric · APM (Trace & Span Analytics, Error Tracking, SLOs) · Log · Synthetic (API e Browser Tests) · Composite (AND, OR, NOT).
- **Fadiga de alerta**: excesso de falsos positivos ou alertas de baixa prioridade faz as pessoas **ignorarem** os alertas. Remédios: ajustar thresholds, janelas apropriadas, "monitore muitas coisas, mas alerte seletivamente", priorizar.
- **Boas práticas**: acionáveis (com [[Runbook]]) · contexto · revisão contínua · SLOs como guia ([[Error Budget]]) · documentação.

Aparece em: [[MAV 05 - Criando alertas com DD]], [[MAV 10 - Configurando alertas]]
