---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [Provider, Providers, Terraform provider, required_providers, HashiCorp Registry]
---

# Providers do Terraform

**Plugins** que implementam as APIs de uma plataforma e traduzem o HCL em operações concretas (criar, atualizar, destruir). São **"pontes"** com nuvens, DNS, autenticação etc., e tornam o Terraform **multicloud e agnóstico**. São mantidos pela HashiCorp ou pela comunidade.

- **Declaração**: `provider "aws" { region = "us-east-1" }` e `provider "kubectl" {}` (da comunidade, para aplicar arquivos do Kubernetes).
- **Credenciais**: no código (não recomendado), em variáveis de ambiente ou em arquivos de configuração locais.
- **Instalação automática** desde o Terraform **0.13**, a partir do **HashiCorp Registry**.
- **Boas práticas**: fixar versões (`required_providers`) · nada de credenciais no código (variáveis de ambiente ou **HashiCorp Vault**) · dividir em arquivos e módulos · estado remoto.

Aparece em: [[TF 02 - Providers e backend]], [[TF 08 - Criação de infra com AWS]]
