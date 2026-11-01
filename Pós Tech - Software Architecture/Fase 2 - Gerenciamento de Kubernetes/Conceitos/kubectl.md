---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Kube Control, kubeconfig]
---

# kubectl

O **CLI para interagir com um cluster Kubernetes**: a ferramenta principal de administradores e devs para **implantar, atualizar, gerenciar objetos, ver o status e depurar** (logs, conectar a um contêiner). Também chamado **Kube Control**, funciona como **client do nó master**, "sem dúvida a forma mais produtiva" de trabalhar com o Kubernetes.

- Roda na máquina local e fala com o cluster pela **API do Kubernetes** (RESTful: GET, POST, PUT, DELETE). A API é dividida em **grupos**, e o **"core"** tem os recursos fundamentais (pods, serviços, replicaset).
- O **kubeconfig** guarda o **endereço do servidor da API**, as **credenciais** e o **contexto** atual.
- Rodar `kubectl` sem parâmetros lista as opções: comandos **básicos, intermediários, de implantação e de gerenciamento**.

**Comandos que aparecem nas aulas**
| Comando | Para quê | Aula |
|---|---|---|
| `kubectl version --output=yaml` | Validar a instalação | [[K8S1 01 - Introdução ao Kubernetes]] |
| `kubectl run nginx --image=nginx:1.14.2 --port:80` (assim no PDF) | Criar um pod | [[K8S1 02 - kubectl e a API do Kubernetes]] |
| `kubectl get pods` / `kubectl delete pod nginx` | Listar / remover pods | K8S1 01 e 02 |
| `kubectl get hpa` | Ver se o HPA mudou as réplicas | [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]] |
| `kubectl apply -f <arquivo>.yaml` | Criar recursos a partir de YAML | [[K8S2 01 - Jobs e CronJobs]] em diante |
| `kubectl get svc` | Ver os services | [[K8S2 02 - Logs e monitoramento com EFK]] |
| `kubectl delete statefulsets es-cluster` | Remover o StatefulSet | K8S2 02 |
| `kubectl get clusterrole` / `get rolebinding` / `auth can-i get pods --as tadriano` | Conferir permissões RBAC | [[K8S2 08 - Segurança do AWS EKS]] |

No **EKS**, o kubectl precisa ser **instalado e configurado** para o cluster ([[K8S2 04 - EKS]]).

Aparece em: [[K8S1 01 - Introdução ao Kubernetes]], [[K8S1 02 - kubectl e a API do Kubernetes]]
