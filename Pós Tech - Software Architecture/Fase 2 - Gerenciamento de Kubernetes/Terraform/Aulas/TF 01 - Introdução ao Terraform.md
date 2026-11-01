---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 1
fonte: "POSTECH - Aula1_rev2.pdf"
---

# TF 01 - Introdução ao Terraform

[[Terraform]] · Próxima → [[TF 02 - Providers e backend]]

> [!summary] Em uma frase
> O **Terraform**, da **HashiCorp**, é uma ferramenta de **[[Infraestrutura como Código (IaC)|infraestrutura como código]]** que gerencia, provisiona e orquestra recursos em vários provedores de nuvem e data centers, de forma **declarativa**, escrita em **[[HCL (HashiCorp Configuration Language)|HCL]]**.

## Hands On
Conhecer o Terraform e instalá-lo localmente, para criar a primeira infraestrutura por código.

## Terraform e IaC
- **Terraform**: ferramenta de IaC da **HashiCorp** para **gerenciar, provisionar e orquestrar** recursos em diferentes provedores de nuvem, data centers locais e outras plataformas. A abordagem **declarativa** facilita ambientes complexos, com mais controle, consistência e eficiência.
- **IaC**: a infraestrutura é **definida e gerenciada por código**, em vez de configurações manuais ou scripts ad hoc.

| Benefício da IaC | O que significa |
|---|---|
| **Automação** | Menos tarefas manuais repetitivas |
| **Consistência** | Menos erros humanos e menos diferenças entre ambientes |
| **Escalabilidade** | Facilidade para gerenciar ambientes grandes |
| **Rastreamento** | Histórico de alterações pelo controle de versão |

- **Ferramentas de IaC mais conhecidas**: **Terraform, Ansible, Chef, CloudFormation**. O Terraform se destaca pela **integração com muitos provedores** e pela linguagem simples (**HCL**).

## HCL (HashiCorp Configuration Language)
- A linguagem de configuração de várias ferramentas da HashiCorp: **Terraform, Nomad, Consul**.
- **Declarativa, legível por humanos e fácil de interpretar por máquinas**. Suporta **expressões, variáveis, loops e condicionais**.

| Característica | Ideia |
|---|---|
| **Legibilidade** | Sintaxe próxima de JSON e YAML, com mais expressividade. Declara o **estado desejado**, em vez de etapas (imperativo) |
| **Declarativo** | Você descreve **o que** quer, e a ferramenta cuida de **como** |
| **Extensível e estruturado** | Blocos, atributos, argumentos, expressões; lógica condicional e interpolação |
| **Compatível com JSON** | Qualquer configuração HCL pode ser convertida para JSON |

### Elementos do HCL
**Blocos**: a estrutura básica, definida por **tipo e nome**.
```hcl
resource "aws_eks_cluster" "eks_cluster_fiap" {
  name     = "fiap-eks"
  role_arn = var.awsAcademyRole

  vpc_config {
    subnet_ids         = ["${var.subnetA}", "${var.subnetB}", "${var.subnetC}"]
    security_group_ids = ["${var.securityGroupId}"]
  }

  access_config {
    authentication_mode = "API_AND_CONFIG_MAP"
  }
}
```
- `resource` é o **tipo do bloco**; `"aws_eks_cluster"` é o **tipo de recurso**; `"eks_cluster_fiap"` é o **identificador**.
- **Atributos e argumentos**: propriedades dentro do bloco (`name`, `role_arn`).
- **Sub-blocos**: configurações adicionais (`vpc_config` para a rede; `access_config` para a autenticação).

**Variáveis**: reutilizam valores e abstraem partes da configuração.
```hcl
variable "awsAcademyRole" {
  default = "arn:aws:iam::xxxxxxxxxxx:role/LabRole"
}
```

**Interpolação**: combina valores ou gera strings dinâmicas (ex.: `"${var.subnetA}"`). Código-fonte 3 do PDF:
```hcl
resource "aws_eks_access_entry" "eks_cluster_access_entry" {
  cluster_name      = aws_eks_cluster.eks_cluster_fiap.name
  principal_arn     = var.principalArn
  kubernetes_groups = ["group-1", "group-2"]
  type              = "STANDARD"
}
```

**Condicionais e funções**:
```hcl
subnet_ids = [for subnet in data.aws_subnet.subnet : subnet.id if subnet.availability_zone != "${var.regionDefault}"]
```

A apostila fecha recomendando práticas como **modularização** e **controle de versão**.

## Referências
HashiCorp: Instalação do Terraform, Intro Terraform, O que é Terraform?
