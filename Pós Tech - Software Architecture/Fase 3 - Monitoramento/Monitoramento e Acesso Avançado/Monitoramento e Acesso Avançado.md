---
tags: [pos-tech/fase-3, monitoramento, indice]
disciplina: Monitoramento e Acesso Avançado
fase: 3
aulas: 12
---

# Monitoramento e Acesso Avançado

[[Fase 3 - Monitoramento]] · Revisão → [[Revisão - Monitoramento e Acesso Avançado]]

Autor dos PDFs (quando consta na capa): **Douglas Lima da Silva Martins**. As aulas 5, 6, 9, 11 e 12 não trazem nome.

> [!note] Numeração interna
> Os PDFs 7, 8, 9 e 10 trazem, no cabeçalho, "AULA 05", "06", "07" e "08". Aqui vale a numeração do nome do arquivo.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[MAV 01 - O que é APM e seus benefícios]] | [[SLI, SLO e SLA]], [[Error Budget]] |
| 2 | [[MAV 02 - Introdução APM Datadog]] | [[Datadog]], [[Sidecar]] |
| 3 | [[MAV 03 - Logs com Datadog]] | [[Severidade e Tipos de Logs]] |
| 4 | [[MAV 04 - Infra com Datadog]] | [[Datadog]] (Host Map) |
| 5 | [[MAV 05 - Criando alertas com DD]] | [[Monitors do Datadog]], [[Runbook]] |
| 6 | [[MAV 06 - Criando dashboards com DD]] | [[Dashboards do Datadog]] |
| 7 | [[MAV 07 - Introdução APM New Relic]] | [[New Relic]], [[Apdex]] |
| 8 | [[MAV 08 - Logs com New Relic]] | [[Logs in Context]] |
| 9 | [[MAV 09 - Infra com New Relic]] | [[NRQL]] |
| 10 | [[MAV 10 - Configurando alertas]] | [[Runbook]], [[SLI, SLO e SLA]] |
| 11 | [[MAV 11 - Criando dashboards com New Relic]] | [[NRQL]] |
| 12 | [[MAV 12 - Contexto Map New Relic]] | [[New Relic]] (Service Maps, Workloads) |

## Datadog × New Relic nas aulas
| Tema | Datadog | New Relic |
|---|---|---|
| APM | Aula 2 (status codes, [[Sidecar]]) | Aula 7 ([[Apdex]]) |
| Logs | Aula 3 (severidade e tipos) | Aula 8 ([[Logs in Context]]) |
| Infraestrutura | Aula 4 (Host Map, cloud) | Aula 9 (boas práticas, [[NRQL]]) |
| Alertas | Aula 5 ([[Monitors do Datadog]]) e aula 10 | Aula 10 (políticas e incidentes) |
| Dashboards | Aula 6 (Timeboards e Screenboards) | Aula 11 (widgets com NRQL) |
| Mapas | — | Aula 12 (Service Maps) |

A tabela é só um mapa de navegação, montado a partir dos títulos e do conteúdo das aulas.

## Ligações com outras disciplinas
- **Monitoramento e Acesso (Fase 3)**: o Zabbix, o Prometheus e o Grafana são citados na aula 4 como as ferramentas open source frente ao All-in-One.
- **Terraform (Fase 2)**: a aula 10 recomenda automatizar a criação de alertas com o [[Terraform]].
- **OpenTelemetry (Fase 2)**: a aula 8 cita a **integração OpenTelemetry** como uma das formas de relatar logs ao New Relic, e a aula 1 cita Tracing e OpenTelemetry no resumo.

## Material
PDFs em `~/Desktop/Monitoramento e Acesso Avançado/` ("SOAT - Fase 3 - Monitoramento e acesso avançado - Aula N_rev2.pdf"; a aula 10 começa com "10SOAT").
