---
tags: [pos-tech/fase-3, monitoramento, datadog, apm, conceito]
aliases: [DD, Datadog APM, Datadog Agent]
---

# Datadog

Plataforma de **APM** e monitoramento usada nas aulas 2 a 6 e 10.

| Área | O que as aulas mostram |
|---|---|
| **APM** ([[MAV 02 - Introdução APM Datadog]]) | O **Agent do Datadog APM** em aplicações .NET e NodeJS via container; instrumentação no **mesmo host** ou por [[Sidecar]]; **métricas de rastreamento** (requisições, erros e latência, sobre **100% do tráfego**) e dashboards e alertas por **status code** (4xx × 5xx) |
| **Logs** ([[MAV 03 - Logs com Datadog]]) | Ingestão de logs, **drop rules** e **patterns**; [[Severidade e Tipos de Logs]] |
| **Infraestrutura** ([[MAV 04 - Infra com Datadog]]) | **Host Map** (cinza, vermelho, laranja, verde), containers e imagens (até vulnerabilidades), **integração com cloud** cobrada por ingest e **catálogo de recursos** |
| **Alertas** ([[MAV 05 - Criando alertas com DD]]) | [[Monitors do Datadog]] |
| **Dashboards** ([[MAV 06 - Criando dashboards com DD]]) | [[Dashboards do Datadog]] |

- Segundo a aula 4, mesmo com ferramentas open source como Grafana, Prometheus e Zabbix, muitas empresas adotam a prática de **All-in-One**, ainda que custe um pouco mais.
- Comparado com o [[New Relic]] na aula 7.

Aparece em: [[MAV 02 - Introdução APM Datadog]] a [[MAV 06 - Criando dashboards com DD]], [[MAV 10 - Configurando alertas]]
