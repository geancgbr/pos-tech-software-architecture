---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Service, Services, ClusterIP, NodePort, LoadBalancer, Ingress]
---

# Service do Kubernetes

Expõe **um conjunto de Pods como um serviço**, com **um único ponto de entrada**, e **distribui o tráfego** entre eles (carga balanceada). Criado por um **manifesto YAML** com o tipo, o **seletor** dos Pods e as portas e protocolos.

| Tipo | Expõe em | Acesso | Útil para |
|---|---|---|---|
| **ClusterIP** (**padrão**) | IP interno do cluster | **Só dentro** do cluster | Serviços que conversam com outros serviços do cluster |
| **NodePort** | Uma porta do nó | **Fora**, pelo IP do nó + porta | Serviços acessados de fora, como aplicativos web |
| **LoadBalancer** | Um balanceador de carga externo | **Fora**, por um IP externo + porta | Acesso externo com balanceamento de carga |

**Exemplos nas aulas**
- `elasticsearch` com `clusterIP: None` e `kibana-np` do tipo **NodePort** (`nodePort: 30000`), cada um servindo "como um DNS" ([[K8S2 02 - Logs e monitoramento com EFK]]).
- `my-nodejs-app-service` do tipo **LoadBalancer** (porta 80 → 3000) ([[K8S2 05 - AWS EKS na prática, parte 1]]).

**Ingress** (parte 2, aula 5): configura o **roteamento do tráfego externo** para o aplicativo, se necessário. No exemplo, associa o domínio `my-nodejs-app.example.com` ao service na porta 80.

Aparece em: [[K8S1 04 - Services e ConfigMap]], [[K8S2 05 - AWS EKS na prática, parte 1]]
