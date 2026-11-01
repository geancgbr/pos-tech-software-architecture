---
tags: [pos-tech/fase-3, monitoramento, newrelic, logs, conceito]
aliases: [Logs contextualizados, Log decoration, Logs in context]
---

# Logs in Context

Recurso do [[New Relic]] que mostra os logs **no contexto** de outras telas (APM, infraestrutura, distributed tracing, **Errors Inbox**), disponível via **APM agent**, **agent de infraestrutura** ou **integração OpenTelemetry** ([[MAV 08 - Logs com New Relic]]).

- Reúne dados de aplicativos e infraestrutura numa única solução, para chegar à **causa raiz** mais rápido.
- **Habilitado por padrão** no APM, o que **pode** impactar segurança, conformidade, faturamento ou desempenho.
- **Três opções no .NET**: (1) **encaminhamento pelo agente** (o mais simples; `span.id`, `trace.id`, `hostname`, `entity.guid`, `entity.name`; agente 9.7.0+, padrão desde 9.8.0) · (2) **log decoration** com encaminhador externo (5 atributos; não usar com o encaminhamento do agente, senão **cobrança dupla**) · (3) enviar os metadados pelo aplicativo (**não mais incentivado**).
- **Limitações**: fora do Node.js, o forward não envia o log completo; sem stack trace nos agentes Java e .NET; metadados do Fluentd e do Kubernetes não aparecem no aplicativo.

Aparece em: [[MAV 08 - Logs com New Relic]]
