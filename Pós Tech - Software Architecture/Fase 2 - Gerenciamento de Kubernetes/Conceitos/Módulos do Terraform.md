---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [Módulo Terraform, module, Terraform Registry]
---

# Módulos do Terraform

A **unidade de organização e reutilização** da IaC: encapsulam recursos, variáveis e saídas. Assim como **funções** em linguagens de programação, os módulos **evitam duplicação de código**.

- **Locais** (`source = "./modulos/ec2"`) ou **remotos** (ex.: Terraform Registry). O exemplo da aula usa `terraform-aws-modules/ec2-instance/aws`, da HashiCorp, da comunidade ou próprios.
- **Estrutura**: `main.tf` · `variables.tf` · `outputs.tf`.
- **Benefícios**: reutilização · padronização · menos erros · escalabilidade (evita projeto monolítico) · documentação.
- **Boas práticas**: **fixar versão** · um objetivo por módulo · testar isoladamente · documentar · evitar hardcoding · `terraform validate` periódico.

Exemplos: [[TF 06 - Módulos]]
