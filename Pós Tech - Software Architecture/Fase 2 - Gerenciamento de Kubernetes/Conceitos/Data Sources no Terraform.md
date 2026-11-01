---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [Data source, Data sources, Bloco data]
---

# Data Sources no Terraform

Um bloco **`data`** que **consulta** informações de recursos existentes (em provedores, APIs públicas ou infraestrutura de outras equipes) **sem criar nem alterar nada**. É **somente leitura** e dinâmico.

- **Sintaxe**: `data "<provider>_<resource_type>" "<name>" { ... }` (ex.: `data "aws_iam_role" "labrole" { name = "LabRole" }`).
- **Uso**: o `<name>` serve para referenciar os dados no código (ex.: `data.aws_ami.latest_amazon_linux.id`, com `most_recent = true`, `filter` e `owners`).
- É resolvido na fase de **plan**. Pode depender de outros recursos (ex.: uma sub-rede de uma VPC gerenciada pelo Terraform).
- Diferença para os [[Variáveis, Outputs e Locals no Terraform|locals]]: os data sources tratam de **dados externos**, e os locals, de **valores internos** derivados.

Exemplo da AMI: [[TF 05 - Data e locals#Data sources]]
