---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [terraform init, terraform plan, terraform apply, terraform destroy, terraform validate, terraform import, terraform fmt, terraform refresh]
---

# Comandos do Terraform

**Fluxo principal**: `init` (sempre o primeiro: providers e backend) → `validate` (sintaxe) → `plan` (mostra o que muda, **sem alterar**) → `apply` (executa, atualiza o tfstate, pede confirmação) → `destroy`.

**Outros**: `show` (estado) · `output` (valores dos blocos output) · `refresh` (sincroniza o estado com a infraestrutura real) · `state` (`mv`, `rm`, `list`) · `fmt` (formatação) · `graph` (dependências em DOT, com Graphviz) · `import` (traz recursos criados fora do Terraform).

**Parâmetros**: `-auto-approve` · `-var-file` · `-target`.

Tabela completa, com quando usar cada um: [[TF 03 - Principais comandos#Os comandos]]
