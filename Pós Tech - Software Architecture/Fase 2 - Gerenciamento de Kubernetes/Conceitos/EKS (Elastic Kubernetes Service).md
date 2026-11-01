---
tags: [pos-tech/fase-2, terraform, kubernetes, conceito, aws]
aliases: [EKS, Amazon EKS, Elastic Kubernetes Service, Node Group, Node Groups]
---

# EKS (Elastic Kubernetes Service)

## Na disciplina Terraform (aula 8)
Serviço **gerenciado pela AWS para executar clusters Kubernetes**. Configurado via Terraform, a automação é mais robusta, repetível e consistente.

**O que se cria para ter um cluster**: provider AWS · **VPC** (10.0.0.0/16), subnets pública e privada, internet gateway · **role IAM do cluster** (`eks.amazonaws.com`) e **role do node group** (`ec2.amazonaws.com`) · **`aws_eks_cluster`** · **`aws_eks_node_group`** (instâncias EC2 que executam os workloads; t3.medium, 1 a 3 nós, 2 desejados) · **access entry** e **policy association** (AmazonEKSClusterAdminPolicy) · output **kubeconfig** para o **kubectl**.

**Verificação**: AWS Console → EKS, e `kubectl get nodes`.

Detalhes: [[TF 08 - Criação de infra com AWS]]. O HCL da aula 1 também usa um `aws_eks_cluster` como exemplo ([[TF 01 - Introdução ao Terraform]]).

## Na disciplina Kubernetes (parte 2, aulas 4 a 9)
**Serviço gerenciado da AWS** para executar aplicativos em contêineres com o Kubernetes, **sem gerenciar a infraestrutura subjacente**.
- Usa as **ferramentas e APIs padrão do Kubernetes**: tudo o que se aprendeu no ambiente local vale no EKS.
- **A AWS** gerencia servidores, rede e armazenamento; **você** gerencia os aplicativos.
- **Altamente escalável e altamente disponível**.
- **Por que nuvem**: sem provisionamento de hardware e sem custo de gestão (hardware e software).
- **Criação pela console**: "Criar cluster" → implementação **rápida** ou **personalizada** → nome e região → VPC → versão do Kubernetes → "Criar" → conectar com o [[kubectl]]. No Hands On, também com o **AWS CDK** (IaC).
- **Rede**: **Amazon VPC CNI** (padrão e recomendada; Pods com IPs privados da VPC) ou **Calico** (terceiros; separação de tráfego entre namespaces).
- **Control plane** e **worker nodes**: ver [[Cluster Kubernetes]].
- **Na prática**: migração de um sistema do IIS para o EKS, HPA com K6, CI/CD, [[RBAC no Kubernetes|IAM e RBAC]] e monitoramento com [[Amazon CloudWatch|CloudWatch]], [[Prometheus]] e [[Grafana]].

Aparece em: [[TF 08 - Criação de infra com AWS]], [[K8S2 04 - EKS]] a [[K8S2 09 - Monitoramento e logging do EKS]]
