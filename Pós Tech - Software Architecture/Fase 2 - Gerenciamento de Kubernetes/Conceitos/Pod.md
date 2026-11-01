---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Pods, Rótulos, Labels, Anotações, Annotations]
---

# Pod

**Abstração que representa um único processo em execução** no cluster. Tem **um ou mais contêineres** que compartilham **o mesmo espaço de rede e armazenamento** (ex.: um contêiner web e um banco de dados pela mesma interface de rede). Na aula 1: cada nó do cluster pode ter um ou mais contêineres, chamado de "POD".

- **Efêmeros**: criados e destruídos conforme a necessidade.
- Criados a partir de **YAML ou JSON** (contêineres, imagens, portas). Recebem um **IP interno** no cluster.
- **Escala horizontal**: vários Pods idênticos dividindo a carga.

**Rótulos × anotações**
| | Rótulos (labels) | Anotações (annotations) |
|---|---|---|
| O que são | Pares chave-valor | Pares chave-valor **opcionais** |
| Para quê | **Identificar, categorizar e selecionar** objetos (escalonamento, exclusão) | **Metadados**: depuração, documentação, políticas de segurança |
| Usados em seleção? | Sim | **Não** |
| Exemplo | `app: myapp` | `author: Thiago S Adriano` |

Os rótulos são usados pelo **seletor de rótulo** dos [[ReplicaSet e Deployment|ReplicaSets e Deployments]].

**Pods de Job**: quando um Job termina, o Kubernetes **remove automaticamente** os Pods dele. Os Pods "comuns" continuam UP até uma interação nossa ([[Jobs e CronJobs]]).

Aparece em: [[K8S1 01 - Introdução ao Kubernetes]], [[K8S1 03 - Pods, rótulos e anotações]]
