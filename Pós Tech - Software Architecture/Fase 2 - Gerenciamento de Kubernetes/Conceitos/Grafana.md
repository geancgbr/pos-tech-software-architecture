---
tags: [pos-tech/fase-2, kubernetes, observabilidade, conceito]
aliases: [grafana]
---

# Grafana

## Na disciplina Kubernetes
Plataforma de **análise e visualização de dados de código aberto** para criar e compartilhar **painéis e alertas personalizados** de métricas, em tempo real.

- Suporta vários bancos de métricas, **incluindo o [[Prometheus]]**, cujas métricas visualiza em painéis de saúde e desempenho.
- **Alertas personalizados** com base em métricas específicas, para que as equipes de operações sejam notificadas **antes que os problemas se tornem críticos**.
- **EKS + Prometheus + Grafana**: coletar e visualizar as métricas dos recursos Kubernetes em tempo real. → [[K8S2 09 - Monitoramento e logging do EKS]]

## Na disciplina OpenTelemetry
- **Aula 3**: o Grafana é conectado ao Prometheus num dashboard com os indicadores **RED** (taxa de requisições, erros e duração).
- **Aula 4** (segundo o resumo): consultas em **LogQL** aos logs do [[Grafana Loki]], e os **"Derived Fields"** criam um link direto de cada linha de log para o trace no [[Jaeger]].
- **Aula 5**: o alerta da narrativa de depuração aparece num gráfico do Grafana alimentado pelo Prometheus. Uma mitigação da curva de aprendizagem é ter **dashboards padronizados** no Grafana. → [[OTEL 05 - Boas práticas e desafios]]

## Na Fase 1
No Hands On de [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], com o Prometheus.

## Na disciplina Monitoramento e Acesso (Fase 3)
O Grafana recebe o **Loki como data source** (**Connections → Data sources**, URL `http://localhost:3100`, **Save & test**) e mostra os logs num **dashboard**, filtrados pelos **labels** do Promtail. → [[MON 03 - Prometheus e Grafana]]

Aparece em: [[K8S2 09 - Monitoramento e logging do EKS]], [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]], [[OTEL 04 - OpenTelemetry Logs (Loki)]], [[OTEL 05 - Boas práticas e desafios]], [[MON 03 - Prometheus e Grafana]]
