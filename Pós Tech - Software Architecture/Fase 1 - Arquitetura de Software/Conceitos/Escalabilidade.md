---
tags: [pos-tech/fase-1, arquitetura, conceito, atributo-de-qualidade]
aliases: [Scalability, Software escalável]
---

# Escalabilidade

**Capacidade de o sistema crescer e se adaptar a um aumento de demanda** (usuários, dados, tráfego de rede) **sem prejudicar desempenho ou confiabilidade**.

**Estratégias**
- **Arquitetura escalável**: sistemas distribuídos e balanceamento de carga.
- **Tecnologias modernas**: computação em nuvem e contêineres.
- **Banco de dados escalável**: NoSQL e tecnologias de cache ([[Estratégias de Cache]]).
- **Monitoramento e otimização** frequentes, para o longo prazo.

**Ferramentas de monitoramento e otimização citadas**: New Relic, Nagios, Splunk, AppDynamics e VisualVM (Java). A descrição de cada uma está em [[ARQ 04 - Escalabilidade, disponibilidade e desempenho#Ferramentas de monitoramento e otimização]].
**No Hands On**: health check, Zabbix, Prometheus e Grafana (com Docker) e Azure Container Apps (PaaS para Kubernetes) para escalar.

A escalabilidade também aparece como uma das dimensões do [[Desempenho]].

## Na disciplina Kubernetes (Fase 2)
- **Escalabilidade (scaling)**: a capacidade de **crescer ou encolher** a infraestrutura conforme a demanda (exemplo da **Black Friday**).
- **Horizontal**: criar e destruir recursos computacionais **por demanda**. **Vertical**: **expandir os recursos físicos** (on-premise ou nuvem). → [[K8S1 01 - Introdução ao Kubernetes]]
- No Kubernetes, o [[HPA (Horizontal Pod Autoscaler)|HPA]] ajusta automaticamente as réplicas, e o [[ReplicaSet e Deployment|Deployment]] tem dimensionamento horizontal.

## Na disciplina Data Engineering (Fase 4)
Nos **bancos relacionais**, a escalabilidade **vertical** (mais recursos num único servidor) foi a predominante; os **não relacionais** são projetados para a **horizontal** (dados distribuídos em vários servidores) ([[DE 01 - Fundamentação e SGBDs]]). Os DBaaS oferecem escalabilidade automática **vertical e horizontal** ([[DE 06 - Cloud e DBaaS]]).

## Na disciplina Resiliência em Microsserviços (Fase 4)
A estratégia de resiliência "principal e mais simples": **balanceamento de carga** e **escalabilidade horizontal**, com **auto-scaling** e **health checks** ([[RES 01 - Introdução à resiliência]]).

Aparece em: [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], [[K8S1 01 - Introdução ao Kubernetes]], [[DE 01 - Fundamentação e SGBDs]], [[DE 06 - Cloud e DBaaS]], [[RES 01 - Introdução à resiliência]]
