---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 8
fonte: "POSTECH - Aula8_rev2.pdf"
---

# TF 08 - Criação de infra com AWS

← [[TF 07 - Loops e expressões]] · [[Terraform]] · Próxima → [[TF 09 - Terraform Cloud]]

> [!summary] Em uma frase
> A aula junta tudo para criar um **cluster [[EKS (Elastic Kubernetes Service)|EKS]]** completo com Terraform: **provider AWS, VPC (subnets e internet gateway), roles IAM, cluster, node group, controle de acesso e kubeconfig**, aplicado com `init`, `plan` e `apply`.

## Hands On
A criação "minuciosa" de uma infraestrutura completa do EKS com Terraform.

## Contexto
- No contexto da AWS, o Terraform permite criar e gerenciar **instâncias EC2, VPCs, RDS e clusters EKS**.
- O **EKS (Elastic Kubernetes Service)** é o serviço **gerenciado pela AWS para executar clusters Kubernetes**. Configurado via Terraform, a automação é mais robusta, repetível e consistente.
- A aula também destaca a importância de organizar a infraestrutura em **módulos**.

## Preparação
1. **Instalar o Terraform** (versão mais recente, em terraform.io).
2. **Credenciais da AWS**: `aws configure` (com a AWS CLI) ou variáveis de ambiente. Também dá para usar **perfis da AWS CLI**.

## Os recursos criados
| Passo | Recurso | Detalhe do PDF |
|---|---|---|
| 1 | **Provider** `aws` | `region = var.regionDefault` (us-east-1 como valor da variável) |
| 2 | **VPC** `aws_vpc.main` | CIDR **10.0.0.0/16**, com DNS support e DNS hostnames. Isola os recursos e segmenta a rede |
| 3 | **Subnets** | **Pública** 10.0.1.0/24 (acessível pela internet) e **privada** 10.0.2.0/24 (isolada, para bancos e instâncias internas) |
| 4 | **Internet Gateway** | Permite que os recursos da subnet pública acessem a internet |
| 5 | **Role IAM do cluster** `eks_service_role` | `sts:AssumeRole` para `eks.amazonaws.com`; policies AmazonEKSClusterPolicy, AmazonEKSServicePolicy, AmazonEC2ContainerRegistryReadOnly, AmazonVPCFullAccess. **Permissões para o EKS criar e gerenciar recursos** |
| 6 | **Role IAM do node group** `eks_node_group_role` | `sts:AssumeRole` para `ec2.amazonaws.com`; AmazonEKSWorkerNodePolicy, AmazonEC2ContainerRegistryReadOnly, AmazonVPCFullAccess. Para os nós interagirem com o EKS e serviços como o **ECR** |
| 7 | **Cluster EKS** `aws_eks_cluster.main` | Nome "my-cluster", **role_arn** da role do cluster, subnets pública e privada. É o ponto central do ambiente Kubernetes |
| 8 | **Node Group** `aws_eks_node_group.main` | Instâncias EC2 que **executam os workloads do Kubernetes**: **t3.medium**, `desired_size = 2`, `min_size = 1`, `max_size = 3`, subnet privada, `depends_on` o cluster |
| 9 | **Controle de acesso** | `aws_eks_access_entry` (uma role IAM com os grupos Kubernetes "fiap" e "live", tipo STANDARD) e `aws_eks_access_policy_association` (**AmazonEKSClusterAdminPolicy**, escopo cluster) |
| 10 | **Output kubeconfig** | `aws_eks_cluster.main.kubeconfig`, usado pelo **kubectl** para se conectar ao cluster |

O código completo de cada bloco está nos Códigos-fonte 1 a 8 do PDF.

## Aplicar e verificar
1. `terraform init`, `terraform plan` e `terraform apply`.
2. Verificar no **AWS Management Console → EKS**.
3. Verificar os nós com **`kubectl get nodes`**.

**Benefícios** de usar Terraform na AWS, segundo a aula: **automação, versionamento e consistência**.

## Referências
Terraform Registry (aws_iam_role, aws_vpc) · HashiCorp, *Provision an EKS cluster (AWS)*
