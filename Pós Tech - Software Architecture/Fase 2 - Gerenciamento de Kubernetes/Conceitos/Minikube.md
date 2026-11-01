---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: []
---

# Minikube

Implementação **leve** do Kubernetes que cria uma **VM local** com um cluster de **um nó só**. Segundo a aula, é a **melhor indicação para estudos e desenvolvimento local**.

- Precisa de um mecanismo de virtualização (na aula, o **[[Docker]]**). Verifique os pré-requisitos de hardware.
- `minikube start` baixa uma imagem do Kubernetes do repositório oficial (pode demorar); depois, `kubectl get pods`.

Aparece em: [[K8S1 01 - Introdução ao Kubernetes]]
