---
tags: [pos-tech/fase-3, monitoramento, newrelic, conceito]
aliases: [New Relic Query Language, Newrelic Query Language, NRDB]
---

# NRQL

**Linguagem de consulta New Relic**, **semelhante ao (ANSI) SQL**, para recuperar dados do [[New Relic]] (a base de telemetria **NRDB**).

```
SELECT ... FROM DataType [WHERE] [FACET] [LIMIT] [SINCE] [UNTIL] [COMPARE WITH] [TIMESERIES]
```
- **FROM**: Transaction, PageView, SystemSample, Log, Metric. **FACET** ≈ GROUP BY. **TIMESERIES** gera série temporal.
- **Usos** (aula 9): gráficos · perguntas de troubleshooting ou negócio · **alertas baseados em NRQL** ("nosso tipo de alerta principal e mais poderoso", segundo o texto) · consultas de API · cálculos como **funis**.
- **Dashboards** (aula 11): praticamente tudo é alimentado por NRQL. **Data Explorer** mostra os dados disponíveis; **Query Builder** testa as queries. Evitar `FACET` de alta cardinalidade sem `LIMIT`.
- **Alertas** (aula 10): condições personalizadas com NRQL.

Aparece em: [[MAV 09 - Infra com New Relic]], [[MAV 10 - Configurando alertas]], [[MAV 11 - Criando dashboards com New Relic]]
