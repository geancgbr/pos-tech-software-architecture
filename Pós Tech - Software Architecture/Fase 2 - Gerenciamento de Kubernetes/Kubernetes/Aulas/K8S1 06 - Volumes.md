---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 6
fonte: "Kubernetes/Aula 6.pdf (Thiago Adriano)"
---

# K8S1 06 - Volumes

← [[K8S1 05 - ReplicaSets e Deployments]] · [[Kubernetes]] · Próxima → [[K8S1 07 - Probes]]

> [!summary] Em uma frase
> Armazenar dados é um desafio comum em ambientes de contêineres. O Kubernetes resolve isso com **volumes (VOL)**, **persistent volumes (PV)**, **persistent volume claims (PVC)** e **storage classes (SC)**, que guardam os dados **fora do contêiner**, independentes do ciclo de vida dele. Ver [[Volumes, PV, PVC e StorageClass]].

## Hands On
Os tipos de volumes que podem ser usados com o Kubernetes.

## Volumes (VOL)
- Uma maneira **consistente e portátil** de armazenar **dados persistentes** num cluster, o que torna o gerenciamento de dados mais **fácil e escalável**.
- **Úteis quando os dados precisam sobreviver a reinicializações ou redimensionamentos de Pods**. Exemplo: um contêiner de banco de dados que cai e sobe de novo e precisa das informações que seriam perdidas.

| Tipo de volume | O que é | Uso |
|---|---|---|
| **emptyDir** | Volume **vazio**, criado quando o Pod **inicia** e excluído quando o Pod é **encerrado** | Compartilhar **arquivos temporários** entre contêineres de um Pod |
| **hostPath** | Monta um **diretório ou arquivo do nó** do cluster no contêiner | Quando os contêineres precisam acessar arquivos ou diretórios do nó |
| **persistentVolumeClaim** | Fornece **armazenamento persistente** aos contêineres de um Pod | Quando os dados precisam sobreviver a reinicializações ou redimensionamentos de Pods |

- **Exemplo (Figura 1)**: um Pod com um contêiner que usa um volume **emptyDir** montado em **`/cache`**. Qualquer arquivo nesse diretório é compartilhado entre os contêineres do Pod.

## Persistent Volume (PV)
- Um volume que **sobrevive à reinicialização ou exclusão do Pod** em que foi criado. Pode ser **reutilizado em vários Pods** e tem um **ciclo de vida separado** do Pod.
- Os **administradores do cluster** provisionam os PVs e dão acesso a eles a partir de um Pod: criam o objeto PV e depois definem como ele será usado pelos Pods.

| Tipo de PV | O que é |
|---|---|
| **NFS** | Protocolo de **compartilhamento de arquivos em rede**: vários nós acessam o mesmo armazenamento |
| **iSCSI** | Protocolo de **armazenamento em rede**: monta um armazenamento remoto num nó do cluster |
| **hostPath** | Monta um diretório ou arquivo do nó do cluster no contêiner |
| **EBS (Elastic Block Store)** | Serviço de armazenamento em nuvem da **AWS** para volumes persistentes |

- **Exemplo (Figura 2)**: um PV do tipo **NFS**, com o servidor NFS e o caminho do volume, a **capacidade** de armazenamento e as **políticas de acesso**.

## Persistent Volume Claim (PVC)
- Uma maneira de **solicitar espaço de armazenamento persistente** no cluster. O PVC pede acesso a um volume persistente e especifica as **reivindicações**: o **tamanho** do volume e o **tipo** de armazenamento.
- O Kubernetes usa essas reivindicações para **associar um PV existente ou provisionar um novo**.

| Tipo de PVC | Montado por | Para |
|---|---|---|
| **ReadWriteOnce** | **Um único nó** | Leitura e gravação |
| **ReadOnlyMany** | **Vários nós** | Leitura |
| **ReadWriteMany** | **Vários nós** | Leitura e gravação |

## Storage Class (SC)
- Uma maneira de **definir diferentes tipos de armazenamento** para as necessidades de cada aplicação ou serviço, com **políticas**: tipo de armazenamento, **nível de desempenho** e tamanho.
- Úteis em ambientes de contêiner, em que aplicações diferentes têm necessidades diferentes. Cada aplicação ou serviço pode ter sua política, o que torna o gerenciamento **mais fácil e eficiente**.

| Tipo de SC | Características | Adequado para |
|---|---|---|
| **Standard** | Padrão, oferecido pela maioria dos provedores de nuvem. Pode **não** ter o melhor desempenho ou escalabilidade | Uso geral |
| **SSD** | **Mais rápido e mais escalável** que o padrão | Aplicações com **alto desempenho de E/S**, como bancos de dados |
| **Storage area network (SAN)** | Oferecido por alguns provedores de nuvem; provisiona volumes num **pool compartilhado** | Ambientes de **missão crítica**, com alta disponibilidade e desempenho |

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
