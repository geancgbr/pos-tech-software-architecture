---
tags: [pos-tech/fase-3, monitoramento, indice]
disciplina: Monitoramento e Acesso
fase: 3
aulas: 3
---

# Monitoramento e Acesso

[[Fase 3 - Monitoramento]] · Revisão → [[Revisão - Monitoramento e Acesso]]

Autor dos PDFs: **Douglas Lima da Silva Martins**.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[MON 01 - Introdução ao Zabbix]] | [[Zabbix]], [[Docker Compose]] |
| 2 | [[MON 02 - Monitoramento com Zabbix]] | [[Zabbix]] (hosts, templates, macros), [[ODBC]] |
| 3 | [[MON 03 - Prometheus e Grafana]] | [[Grafana Loki]], [[Promtail]], [[Grafana]] |

## A stack de monitoramento das aulas
| Ferramenta | Papel na disciplina |
|---|---|
| [[Zabbix]] | Monitoramento de bancos de dados via [[ODBC]], sem Agent (a aula 2 cita servidores como algo já monitorado, sem mostrar como) |
| [[Grafana Loki]] + [[Promtail]] | Coleta de **logs**: o Promtail lê e envia, o Loki recebe na porta 3100 |
| [[Grafana]] | Dashboards, com o Loki como data source |

Segundo a aula 3, junto com o Zabbix e o Prometheus, os logs "completam toda uma stack sobre monitoramento".

## Ligações com outras disciplinas
- **Dockerização (Fase 2)**: o Zabbix sobe com [[Docker Compose]], e o Docker depende de [[Cgroups e Namespaces]].
- **OpenTelemetry (Fase 2)**: o [[Grafana Loki]], o [[Prometheus]] e o [[Grafana]] também aparecem lá.
- **Arquitetura de Software (Fase 1)**: o Zabbix é citado na [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]].

## Material
PDFs em `~/Desktop/Monitoramento e Acesso /` ("Aula 01 - Introdução ao Zabbix_revFinal.pdf" a "Aula 03 - Prometheus e Grafana_revFinal.pdf").
