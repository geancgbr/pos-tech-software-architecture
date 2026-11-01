---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Volumes no Kubernetes, Persistent Volume, PV, Persistent Volume Claim, PVC, StorageClass, Storage Class, emptyDir, hostPath]
---

# Volumes, PV, PVC e StorageClass

O armazenamento de dados é um desafio comum em ambientes de contêineres. O Kubernetes oferece **volumes (VOL), persistent volumes (PV), persistent volume claims (PVC) e storage classes (SC)**, que guardam os dados **fora do contêiner**, independentes do ciclo de vida dele.

| Conceito | O que é |
|---|---|
| **Volume** | Forma **consistente e portátil** de armazenar dados persistentes. Útil quando os dados precisam **sobreviver a reinicializações ou redimensionamentos de Pods** |
| **PV** | Volume que **sobrevive à reinicialização ou exclusão do Pod**, reutilizável em vários Pods, com **ciclo de vida separado**. Provisionado pelos **administradores do cluster** |
| **PVC** | **Solicita** armazenamento persistente (tamanho e tipo). O Kubernetes **associa um PV existente ou provisiona um novo** |
| **SC** | Define **tipos de armazenamento** com políticas (tipo, desempenho, tamanho) para cada aplicação ou serviço |

**Tipos**
- **Volumes**: `emptyDir` (vazio, vive enquanto o Pod vive; arquivos temporários entre contêineres) · `hostPath` (diretório ou arquivo do nó) · `persistentVolumeClaim` (armazenamento persistente).
- **PV**: NFS · iSCSI · hostPath · EBS (AWS).
- **Tipos de PVC**: **ReadWriteOnce** (um nó, leitura e gravação) · **ReadOnlyMany** (vários nós, leitura) · **ReadWriteMany** (vários nós, leitura e gravação).
- **SC**: Standard (uso geral) · SSD (alto desempenho de E/S, como bancos) · SAN (pool compartilhado, missão crítica).

**Em outras aulas**: o StatefulSet do Elasticsearch usa `volumeClaimTemplates` com `ReadWriteOnce` e 3Gi, e o DaemonSet do Fluentd usa `hostPath` em `/var/log` ([[K8S2 02 - Logs e monitoramento com EFK]]).

Volumes no Docker: [[Volumes e Containers de Dados]].

Aparece em: [[K8S1 06 - Volumes]]
