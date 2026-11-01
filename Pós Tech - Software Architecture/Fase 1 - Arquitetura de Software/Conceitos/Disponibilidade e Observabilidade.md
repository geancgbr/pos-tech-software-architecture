---
tags: [pos-tech/fase-1, arquitetura, conceito, atributo-de-qualidade]
aliases: [Disponibilidade, Observabilidade, Availability, Observability]
---

# Disponibilidade e Observabilidade

Duas métricas importantes em sistemas de computação e TI.

| | Disponibilidade | Observabilidade |
|---|---|---|
| Definição | Capacidade de o sistema **estar disponível para uso** quando necessário, funcionando e acessível | Capacidade de **observar e medir o comportamento** do sistema **em tempo real**, para monitorar, rastrear e resolver problemas rapidamente |
| Medida | **Tempo de atividade**: o tempo em que o sistema está disponível em relação ao tempo total | **Métricas de desempenho**: tempo de resposta, taxa de erros, utilização de recursos |

**São complementares**: um sistema muito disponível é pouco útil se não puder ser observado, e um muito observável é pouco útil se não estiver disponível. Monitore os dois.

## Na disciplina Kubernetes (Fase 2)
**Monitoramento e observabilidade** permitem entender o que está acontecendo com o sistema, verificar **saúde e erros** e, em estágios mais maduros, **extrair indicadores de negócio**. Ferramentas da disciplina: [[EFK (Elasticsearch, Fluentd e Kibana)|EFK]] para logs (parte 2, aula 2) e, no EKS, [[Amazon CloudWatch|CloudWatch]], [[Prometheus]] e [[Grafana]] (parte 2, aula 9).

## Na disciplina OpenTelemetry (Fase 2)
| | Monitoramento | Observabilidade |
|---|---|---|
| Definição | Observar e coletar **dados pré-definidos** para verificar a saúde | Entender o **estado interno** de um sistema complexo só pelos **outputs externos** (telemetria) |
| Responde | **Se** algo está errado | **Por que** algo está errado, mesmo sem ter previsto o problema |
| Abordagem | **Reativa**: "incógnitas conhecidas" (known unknowns) | **Investigativa**: "incógnitas desconhecidas" (unknown unknowns) |

- **A observabilidade não substitui o monitoramento; ela o aprimora.** Ela se apoia em [[Três Pilares da Observabilidade (Logs, Métricas e Traces)|três pilares]].
- **Cultura**: a observabilidade é **mais que ferramentas, uma mudança cultural**, com responsabilidade compartilhada ("You Build It, You Run It, You Own It"). → [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 05 - Boas práticas e desafios]]

## Na disciplina Estrutura de Microsserviços (Fase 4)
**Cálculo da indisponibilidade anual**: (100% − disponibilidade) × 365 × 24. Com **99%** ao ano, **1% × 365 × 24 = 87,6 horas** ([[MS 02 - Comunicação entre processos com microsserviços]]). APIs síncronas **reduzem a disponibilidade** (cliente e serviço precisam estar disponíveis); a **mensageria** a melhora.

## Na disciplina Resiliência em Microsserviços (Fase 4)
- Resiliência e disponibilidade são relacionadas, mas **não são a mesma coisa**: a disponibilidade é um indicador; a resiliência não é apenas um indicador, mas um conjunto de estratégias para mantê-la ([[RES 01 - Introdução à resiliência]]). Ver [[Resiliência]].
- **Monitoramento** coleta e alerta sobre métricas **conhecidas**; **observabilidade** é entender o estado interno pelas saídas externas; o Chaos Engineering precisa dos dois ([[RES 05 - Chaos Engineering]]).

Aparece em: [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], [[K8S2 02 - Logs e monitoramento com EFK]], [[K8S2 09 - Monitoramento e logging do EKS]], [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 05 - Boas práticas e desafios]], [[MS 02 - Comunicação entre processos com microsserviços]], [[RES 01 - Introdução à resiliência]], [[RES 05 - Chaos Engineering]]
