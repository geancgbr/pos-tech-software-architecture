---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 3
fonte: "Kubernetes/Aula 3.pdf (Thiago Adriano)"
---

# K8S1 03 - Pods, rótulos e anotações

← [[K8S1 02 - kubectl e a API do Kubernetes]] · [[Kubernetes]] · Próxima → [[K8S1 04 - Services e ConfigMap]]

> [!summary] Em uma frase
> Um **[[Cluster Kubernetes|cluster]]** é um grupo de nodes (master e workers) que executam os Pods. O **[[Pod]]** representa um processo em execução, com um ou mais contêineres que compartilham rede e armazenamento. **Rótulos** identificam e selecionam objetos; **anotações** guardam metadados.

## Hands On (vídeos)
Criar um Pod em exemplos práticos e usar rótulos e anotações.

## Cluster
- Um **grupo de nodes que executam os Pods** e outros recursos. Cada node **pode hospedar vários Pods**, que podem se comunicar pelos **IPs internos**.
- **Exemplo da Figura 1**: 3 nodes, um **Master** e dois **Workers**, que hospedam os Pods.
- **Escalável**: aumenta ou diminui nodes e Pods conforme a carga, distribuindo o trabalho para que cada Pod tenha recursos suficientes.

| Componente | Papel |
|---|---|
| **Master node** | O **componente central**: gerencia o cluster e decide **onde e como executar os Pods** |
| **Worker node** | **Executa os Pods** e outros recursos |
| **etcd** | **Banco de dados distribuído** com a configuração e o **estado do cluster** |
| **kubelet** | **Agente em cada node** que gerencia os Pods daquele node |
| **kube-proxy** | **Encaminha o tráfego de rede** para os Pods |

- Os clusters são **configuráveis e personalizáveis**.
- Dividir os aplicativos em Pods distribuídos por vários nodes permite escrever código com **uma única responsabilidade**, coeso e claro. A apostila cita a disciplina de **Arquitetura de Software da Fase 1**.
- O Kubernetes pode **criar ou destruir nodes e Pods** conforme a carga, sem gerência manual.

## Pod
- **Abstração que representa um único processo em execução** no cluster. Pode ter **um ou mais contêineres** que compartilham **o mesmo espaço de rede e armazenamento**. Exemplo: um contêiner web e um banco de dados, pela mesma interface de rede.
- **Efêmeros**: criados e destruídos conforme a necessidade.
- **Como são criados**: a partir de definições **YAML ou JSON**, com os contêineres, as imagens e as portas (Figura 2). Ao ser criado, o Pod recebe um **IP interno** no cluster.
- **Escala horizontal**: vários Pods idênticos para picos de tráfego, com a carga distribuída de forma transparente.
- **Por que importam**: aplicativos escaláveis e resilientes, divididos em unidades com uma única responsabilidade.

## Rótulos × anotações
| | Rótulos (labels) | Anotações (annotations) |
|---|---|---|
| O que são | Pares **chave-valor** atribuídos a objetos (Pods, Serviços, Application Controllers...) | Pares **chave-valor opcionais** |
| Para quê | **Identificar, categorizar e selecionar** objetos para operações como escalonamento e exclusão | Adicionar **metadados**: depuração, documentação, políticas de segurança |
| Usados em seleção? | **Sim** | **Não**, mas são úteis para documentação e auditoria |
| Exemplo | `app: myapp` | `author: Thiago S Adriano` |

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
