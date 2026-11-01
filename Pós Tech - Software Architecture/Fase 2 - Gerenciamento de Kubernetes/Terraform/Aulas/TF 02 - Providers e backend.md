---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 2
fonte: "POSTECH - Aula2_rev2.pdf"
---

# TF 02 - Providers e backend

← [[TF 01 - Introdução ao Terraform]] · [[Terraform]] · Próxima → [[TF 03 - Principais comandos]]

> [!summary] Em uma frase
> Os **[[Providers do Terraform|providers]]** são plugins que ligam o Terraform às plataformas. O **[[tfstate e Backend|tfstate]]** é a "verdade única" do que foi criado, e o **backend** define onde o estado fica: local (o padrão) ou remoto (o recomendado).

## Hands On (vídeos)
Como o tfstate funciona, baixar alguns providers e criar o primeiro **backend remoto**.

## Providers
- Uma das **peças centrais** da arquitetura: componentes que permitem ao Terraform interagir com plataformas e APIs. São **"pontes"** com nuvens públicas, provedores de DNS, sistemas de autenticação etc.
- Tecnicamente, um provider é um **plugin** que implementa as APIs de uma plataforma e **traduz o HCL em operações concretas** (criar, atualizar, destruir). É o que torna o Terraform **multicloud e agnóstico**.
- São mantidos pela **HashiCorp ou pela comunidade**.

```hcl
provider "aws" {
  region = "us-east-1"
}

provider "kubectl" {}
```
Carrega o provider da **AWS** na região indicada e um provider **da comunidade** (`kubectl`) para aplicar arquivos do **Kubernetes** sem sair do Terraform.

- **Autenticação**: as credenciais podem ir **no código (não recomendado)**, em **variáveis de ambiente** ou em **arquivos de configuração locais**.
- **Instalação automática**: desde o **Terraform 0.13**, os providers são instalados automaticamente a partir do **HashiCorp Registry** (o repositório oficial) ou de registries personalizados.

**Boas práticas**
1. **Fixar as versões** (exata ou um intervalo compatível):
```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorpo/aws"   # assim está grafado no PDF
      version = "5.45.0"
    }
    kubectl = {
      source  = "gavinbunney/kubectl"
      version = ">= 1.7.0"
    }
  }
}
```
2. **Segurança das credenciais**: nunca no código. Use variáveis de ambiente ou o **HashiCorp Vault**.
3. **Organização**: dividir em vários arquivos ou módulos.
4. **Estado remoto**: Terraform Cloud, AWS S3 ou Azure Blob Storage.

## tfstate
- Um dos componentes **mais críticos**: armazena o estado da infraestrutura gerenciada e é a **"verdade única"** do que foi criado, atualizado ou destruído.
- É **gerado automaticamente** por comandos como `apply` e `destroy`. É um **arquivo JSON** com identificadores exclusivos dos recursos, atributos de configuração (nomes, tamanhos, IPs), **dependências** entre recursos e metadata interna.

**Como funciona**
1. **Leitura do estado**: carrega o tfstate.
2. **Comparação** com o estado desejado, no HCL.
3. **Criação do plano**: criar, modificar ou destruir.
4. **Atualização do estado** depois das mudanças.

- **Backup e restauração**: perder ou corromper o tfstate dificulta sincronizar a infraestrutura. Faça **backups regulares** e use um **backend remoto seguro**.
- **Bloqueio de estado**: evita que várias pessoas ou processos alterem o estado ao mesmo tempo. Existe em backends como **S3 (com DynamoDB)** e **Terraform Cloud**.

## Backend
A interface que gerencia o estado e as operações relacionadas: **armazenamento** do estado, **bloqueio** e **execução remota**.

| | Local (padrão) | Remoto (recomendado) |
|---|---|---|
| Onde fica | `terraform.tfstate` no diretório do projeto ou num caminho | AWS S3, Azure Blob Storage, Google Cloud Storage, HashiCorp Terraform Cloud |
| Vantagens | Fácil de configurar; ideal para projetos pessoais ou pequenos | Colaboração; criptografia e backups automáticos; **bloqueio**; acesso centralizado |
| Desvantagens | **Sem colaboração**; risco de perda; **sem bloqueio** | Exige configuração inicial; depende de serviços externos |

```hcl
terraform {
  backend "s3" {
    bucket = "fiap-backend-tf"
    key    = "eks/terraform.tfstate"
    region = "us-east-1"
  }
}
```

**Providers, tfstate e backend são os pilares do Terraform.**

## Referências
HashiCorp: Backend, Providers, State
