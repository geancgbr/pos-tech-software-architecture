---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [ReplicaSet, ReplicaSets, Deployment, Deployments, Rolling Update, Rollback]
---

# ReplicaSet e Deployment

| | ReplicaSet | Deployment |
|---|---|---|
| O que é | Garante que um **número específico de réplicas** de um conjunto de Pods esteja em execução **a qualquer momento** | **Gerencia a implantação** de um conjunto de réplicas de um aplicativo |
| Se uma réplica falha | **Inicia uma nova** para substituí-la | O Kubernetes **inicia outra automaticamente** |
| Além disso | Seleciona os Pods do conjunto por um **seletor de rótulo** | **Rolling Update**, **rollback** e **dimensionamento horizontal** |
| Exemplo da aula | `nginx-fiap`, 3 réplicas, seletor `nginx-app` | `nginx-fiap`, 3 réplicas, Pods com rótulo `nginx-app` |

- **Rolling Update**: cria um **novo conjunto de réplicas** com a nova versão e **substitui gradualmente** as antigas, **sem interromper o serviço**.
- **Rollback**: se a atualização der problema, **reverte para a versão anterior**.
- **Qual usar**: os arquivos **não têm muita diferença**, mas no dia a dia se usa mais o **Deployment**, **por conta do seu controle de versão**.
- O PDF diz que os ReplicaSets são "uma extensão do conceito de Deployment".

**Deployments em outras aulas**: o alvo do [[HPA (Horizontal Pod Autoscaler)|HPA]] (`scaleTargetRef`), o `kibana` do EFK e o `my-nodejs-app` (3 réplicas) da migração para o EKS. A parte 2 também usa um **StatefulSet** (`es-cluster`), descrito como uma estrutura de **armazenamento de dados perenes**, e um **DaemonSet** (`fluentd`), para capturar os dados **no nível de nó** ([[K8S2 02 - Logs e monitoramento com EFK]]).

Aparece em: [[K8S1 05 - ReplicaSets e Deployments]], [[K8S2 05 - AWS EKS na prática, parte 1]], [[K8S2 06 - AWS EKS na prática, parte 2]]
