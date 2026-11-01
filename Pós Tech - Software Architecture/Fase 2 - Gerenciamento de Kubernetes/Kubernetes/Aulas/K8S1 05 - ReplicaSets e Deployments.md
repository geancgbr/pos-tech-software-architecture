---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 5
fonte: "Kubernetes/Aula 5.pdf (Thiago Adriano)"
---

# K8S1 05 - ReplicaSets e Deployments

← [[K8S1 04 - Services e ConfigMap]] · [[Kubernetes]] · Próxima → [[K8S1 06 - Volumes]]

> [!summary] Em uma frase
> O **ReplicaSet** garante que um **número específico de réplicas** de um conjunto de Pods esteja sempre em execução. O **Deployment** gerencia a implantação de um conjunto de réplicas, com **Rolling Update, rollback e dimensionamento horizontal**. No dia a dia usa-se mais o Deployment, **por conta do controle de versão**. Ver [[ReplicaSet e Deployment]].

## Hands On (vídeos)
Primeira videoaula: o ReplicaSet com exemplos práticos, usando um projeto desenvolvido em aula. Segunda videoaula: o Deployment, mostrando a diferença entre Deployment e ReplicaSet. Para testar a escala, os professores também mostraram um **teste de carga com o K6**.

## ReplicaSet
- Objeto do Kubernetes que **garante que um número específico de réplicas** de um conjunto de Pods esteja em execução **a qualquer momento**. Monitora o status das réplicas e, **se alguma falhar, inicia uma nova** para substituí-la.
- **Figuras 1 e 2 do PDF**: dois contêineres funcionando e um com crash, com o ReplicaSet configurado em **2**. O contêiner que caiu é substituído por um novo, mantendo o número de réplicas configurado.
- Mantém a **integridade do estado** do aplicativo, com um **número mínimo de réplicas** em execução o tempo todo.
- O PDF diz que os ReplicaSets são **"uma extensão do conceito de Deployment"** e permitem gerenciar o número de réplicas e atualizar o aplicativo para uma nova versão.
- **Seleção dos Pods**: por um **seletor de rótulo** (ver [[K8S1 03 - Pods, rótulos e anotações#Rótulos × anotações]]). Exemplo: selecionar todos os Pods com o rótulo `app = nginx` para criar réplicas do servidor web nginx.
- **Arquivo de exemplo (Figura 3)**: um ReplicaSet chamado **"nginx-fiap"** com **3 réplicas**, com o seletor **"nginx-app"**.

## Deployment
- Objeto do Kubernetes que **gerencia a implantação de um conjunto de réplicas** de um aplicativo, com recursos de **atualização, rollback e dimensionamento horizontal**.
- O usuário especifica o número de réplicas e o Kubernetes monitora o estado delas. **Se uma réplica falhar ou ficar indisponível, ele inicia outra automaticamente.**

| Recurso | Como funciona |
|---|---|
| **Rolling Update** | Numa atualização, o Kubernetes cria um **novo conjunto de réplicas** com a nova versão e **substitui gradualmente** as antigas, **sem interromper o serviço** |
| **Rollback** | Se ocorrer um problema na atualização, permite **reverter para a versão anterior** |
| **Dimensionamento horizontal** | Aumentar ou diminuir o número de réplicas **conforme a demanda**, útil para cargas que flutuam |

- **Arquivo de exemplo (Figura 4)**: um Deployment chamado **"nginx-fiap"** com **3 réplicas**, gerenciando todos os Pods com o rótulo **"nginx-app"**.

## ReplicaSet × Deployment
O arquivo de Deployment **não tem muita diferença** do de um ReplicaSet, mas no dia a dia usamos mais o Deployment **por conta do seu controle de versão**.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
