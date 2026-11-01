---
tags: [pos-tech/fase-2, kubernetes, aws, observabilidade, conceito]
aliases: [CloudWatch, CloudWatch Logs, CloudWatch Logs Insights, CloudWatch Insights]
---

# Amazon CloudWatch

Serviço de **monitoramento e observabilidade da AWS**: coleta, visualiza e analisa **métricas, logs e eventos** de vários recursos da AWS.

- **Métricas do EKS**: criar um **grupo de recursos** do CloudWatch e configurar a coleta no cluster (CLI da AWS ou console). Análise com **painéis personalizados** e **alertas baseados em métricas**.
- **Logs do EKS**: o **agente do CloudWatch** nos Pods ou o **Fluentd** enviando os logs.

| | CloudWatch Logs | CloudWatch Logs Insights |
|---|---|---|
| Papel | **Armazena e pesquisa** logs em escala (EKS, EC2, Lambda e mais) | **Analisa** logs com **consultas ad hoc** |
| Organização / recursos | **Grupos de logs**, cada um com vários **streams** | Filtro, agregação, visualização, consultas em tempo real, dashboards |

Aparece em: [[K8S2 09 - Monitoramento e logging do EKS]]
