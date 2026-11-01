---
tags: [pos-tech/fase-2, kubernetes, indice]
disciplina: Kubernetes
fase: 2
aulas: 17
aliases: [K8S, K8s, Kubernetes Parte II]
---

# Kubernetes

[[Fase 2 - Gerenciamento de Kubernetes]] · Revisão → [[Revisão - Kubernetes]]

Professor: **Thiago Adriano**. São duas partes: **Kubernetes** (8 aulas, prefixo K8S1) e **Kubernetes Parte II** (9 aulas, prefixo K8S2).

> [!summary] O que é o Kubernetes, segundo as aulas
> Uma plataforma **de código aberto para orquestração de contêineres**, para implantar, dimensionar e gerenciar aplicativos em qualquer ambiente. Automatiza **criar e destruir contêineres a partir de imagens** e **manter a infraestrutura operacional**: se um contêiner falha, cabe ao K8S criar outro. É baseado em **[[Cluster Kubernetes|clusters]]**, com os contêineres agrupados em **[[Pod|Pods]]**, e é acessado pela API REST do nó master, normalmente com o **[[kubectl]]**.

## Parte 1
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[K8S1 01 - Introdução ao Kubernetes]] | [[Contêiner]], [[Escalabilidade]], [[Minikube]] |
| 2 | [[K8S1 02 - kubectl e a API do Kubernetes]] | [[kubectl]] |
| 3 | [[K8S1 03 - Pods, rótulos e anotações]] | [[Cluster Kubernetes]], [[Pod]] |
| 4 | [[K8S1 04 - Services e ConfigMap]] | [[Service do Kubernetes]], [[ConfigMap]] |
| 5 | [[K8S1 05 - ReplicaSets e Deployments]] | [[ReplicaSet e Deployment]] |
| 6 | [[K8S1 06 - Volumes]] | [[Volumes, PV, PVC e StorageClass]] |
| 7 | [[K8S1 07 - Probes]] | [[Probes do Kubernetes]] |
| 8 | [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]] | [[HPA (Horizontal Pod Autoscaler)]] |

## Parte 2
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[K8S2 01 - Jobs e CronJobs]] | [[Jobs e CronJobs]] |
| 2 | [[K8S2 02 - Logs e monitoramento com EFK]] | [[EFK (Elasticsearch, Fluentd e Kibana)]] |
| 3 | [[K8S2 03 - Helm]] | [[Helm]] |
| 4 | [[K8S2 04 - EKS]] | [[EKS (Elastic Kubernetes Service)]], [[Cluster Kubernetes]] |
| 5 | [[K8S2 05 - AWS EKS na prática, parte 1]] | Migração do IIS para o EKS, [[Service do Kubernetes]] (Ingress) |
| 6 | [[K8S2 06 - AWS EKS na prática, parte 2]] | [[HPA (Horizontal Pod Autoscaler)]], [[Ferramentas de Teste de Carga (JMeter e K6)\|K6]] |
| 7 | [[K8S2 07 - Kubernetes CI-CD]] | [[Integração Contínua (CI)]], [[Entrega Contínua e Deploy Contínuo]] |
| 8 | [[K8S2 08 - Segurança do AWS EKS]] | [[RBAC no Kubernetes]] |
| 9 | [[K8S2 09 - Monitoramento e logging do EKS]] | [[Amazon CloudWatch]], [[Prometheus]], [[Grafana]] |

## Onde cada objeto aparece
| Objeto | Aula |
|---|---|
| [[Pod]], rótulos e anotações | [[K8S1 03 - Pods, rótulos e anotações]] |
| [[Service do Kubernetes\|Service]] e [[ConfigMap]] | [[K8S1 04 - Services e ConfigMap]] |
| [[ReplicaSet e Deployment\|ReplicaSet e Deployment]] | [[K8S1 05 - ReplicaSets e Deployments]] |
| Volume, PV, PVC e StorageClass | [[K8S1 06 - Volumes]] |
| Probes | [[K8S1 07 - Probes]] |
| HorizontalPodAutoscaler | [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]], [[K8S2 06 - AWS EKS na prática, parte 2]] |
| Job e CronJob | [[K8S2 01 - Jobs e CronJobs]] |
| StatefulSet, DaemonSet, ServiceAccount, ClusterRole, ClusterRoleBinding | [[K8S2 02 - Logs e monitoramento com EFK]] |
| Chart (Helm) | [[K8S2 03 - Helm]] |
| Ingress | [[K8S2 05 - AWS EKS na prática, parte 1]] |
| ClusterRole e RoleBinding (RBAC) | [[K8S2 08 - Segurança do AWS EKS]] |

## Ligações com outras disciplinas
- **Dockerização e GitHub Actions**: o [[Docker]] é pré-requisito do ambiente (aula 1 da parte 1), e na migração para o EKS a imagem vai para o **Amazon ECR** ([[K8S2 05 - AWS EKS na prática, parte 1]]), também visto em [[Repositórios de Imagens Docker]].
- **Terraform**: a aula 8 de Terraform cria um cluster [[EKS (Elastic Kubernetes Service)|EKS]]. Aqui, o EKS é criado pela console da AWS e pelo AWS CDK.
- **Qualidade de Software (Fase 1)**: o K6 e o JMeter, usados para testar o HPA, estão em [[Ferramentas de Teste de Carga (JMeter e K6)]].
- **Arquitetura de Software (Fase 1)**: a aula 3 da parte 1 cita a disciplina ao falar de Pods com uma única responsabilidade. Prometheus e Grafana também aparecem em [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]].

## Material
PDFs em `~/Desktop/Kubernetes/` (parte 1, "Aula 1.pdf" a "Aula 8.pdf") e `~/Desktop/Kubernetes parte 2/` ("Aula 1.pdf" a "Aula 9.pdf").
