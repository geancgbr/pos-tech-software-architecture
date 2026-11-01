---
tags: [pos-tech/fase-2, kubernetes, observabilidade, conceito]
aliases: [prometheus, kube-prometheus, prometheus-operator]
---

# Prometheus

## Na disciplina Kubernetes
Sistema de **monitoramento e alerta de código aberto** que **coleta, armazena e consulta métricas** de sistemas e aplicativos. Foi desenvolvido originalmente pela equipe do **SoundCloud** e é amplamente usado em ambientes Kubernetes.

- **Modelo pull**: os servidores de monitoramento **solicitam as métricas** dos servidores e aplicativos monitorados, em **intervalos regulares**, e as guardam num **banco de séries temporais**.
- **Linguagem de consulta flexível**, gráficos e alertas. Integra com o **[[Grafana]]** para visualização em tempo real.
- **No EKS**: métricas de Pods, contêineres e nós. Pode rodar como um **conjunto de Pods** no cluster. Integrações de terceiros: **kube-prometheus** e **prometheus-operator**. → [[K8S2 09 - Monitoramento e logging do EKS]]
- **Citado também**: para monitorar as **probes** ([[K8S1 07 - Probes]]) e como fonte de **métricas externas** do HPA ([[K8S1 08 - HPA (Horizontal Pod Autoscaler)]]).

## Na disciplina OpenTelemetry (aula 3)
- Sistema de monitoramento e alerta de código aberto, **graduado pela CNCF**, criado na **SoundCloud**. Tornou-se o **padrão de fato** para métricas em ambientes Kubernetes.
- **Modelo pull**: os alvos (targets) **expõem** as métricas num endpoint HTTP (geralmente **`/metrics`**), e o servidor **raspa (scrape)** em intervalos regulares (ex.: a cada 15 s). No **push**, a aplicação envia ativamente.
- **Vantagens do pull**: controle centralizado · resiliência · **descoberta de serviços** (como a API do Kubernetes) · simplicidade do alvo.
- **Arquitetura**: **servidor** (Scraping Engine, **TSDB**, **PromQL Engine**, API HTTP) · **Alertmanager** (agrupa, desduplica e roteia alertas para Slack, e-mail, PagerDuty) · **Exporters** (convertem métricas de sistemas que não usam o formato Prometheus).
- **Com o OpenTelemetry**: o **Prometheus Exporter no SDK** (a aplicação vira alvo) ou o **[[OpenTelemetry Collector]] como ponte** (o Prometheus raspa o Collector). → [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]]
- **Cardinalidade** (aula 5): cada combinação única de labels cria uma **nova série temporal**; nunca usar atributos de alta cardinalidade como labels ([[Cardinalidade]]).

## Na Fase 1
No Hands On de [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], Prometheus e Grafana aparecem para monitoramento e disponibilidade, com containers Docker.

**Na Fase 4**: aparece como exemplo de banco de **séries temporais**, junto com InfluxDB e TimescaleDB ([[DE 01 - Fundamentação e SGBDs]]).

Aparece em: [[K8S1 07 - Probes]], [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]], [[K8S2 09 - Monitoramento e logging do EKS]], [[OTEL 03 - OpenTelemetry Metrics (Prometheus)]], [[OTEL 05 - Boas práticas e desafios]], [[DE 01 - Fundamentação e SGBDs]]
