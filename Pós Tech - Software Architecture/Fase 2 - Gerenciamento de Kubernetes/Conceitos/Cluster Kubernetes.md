---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Cluster, Master node, Worker node, etcd, kubelet, kube-proxy, Control plane, Node]
---

# Cluster Kubernetes

Um **grupo de nodes que executam os Pods** e outros recursos. Cada node **pode hospedar** vários Pods, que podem se comunicar pelos **IPs internos**. É **escalável**: o Kubernetes pode criar ou destruir nodes e Pods conforme a carga.

| Componente | Papel |
|---|---|
| **Master node** | Componente central: gerencia o cluster e decide **onde e como executar os Pods**. Expõe as **APIs REST** acessadas pelo [[kubectl]] |
| **Worker node** | **Executa os Pods** |
| **etcd** | **Banco de dados distribuído** com a configuração e o estado do cluster |
| **kubelet** | **Agente em cada node** que gerencia os Pods daquele node |
| **kube-proxy** | **Encaminha o tráfego de rede** para os Pods |

- Exemplo da aula 3: **3 nodes**, um Master e dois Workers.
- Dividir os aplicativos em Pods distribuídos permite código com **uma única responsabilidade**.

## Na parte 2 (EKS)
- **Control plane**: o **componente central** do Kubernetes, que **gerencia o estado do cluster** e **coordena os worker nodes**. No EKS, sua configuração inclui a versão do Kubernetes, opções de segurança e autenticação e autorização.
- **Worker nodes**: os **servidores que executam os Pods**. Configuram-se tipo, tamanho e número de instâncias, segurança e armazenamento. → [[K8S2 04 - EKS]]

Para estudos e desenvolvimento local: [[Minikube]] (cluster de um nó só).

Aparece em: [[K8S1 01 - Introdução ao Kubernetes]], [[K8S1 03 - Pods, rótulos e anotações]], [[K8S2 04 - EKS]]
