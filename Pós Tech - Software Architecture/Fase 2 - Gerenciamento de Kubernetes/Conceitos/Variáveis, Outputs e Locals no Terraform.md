---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [Variáveis no Terraform, variable, output, locals, tfvars, TF_VAR_, sensitive]
---

# Variáveis, Outputs e Locals no Terraform

| Tipo | Bloco | Para quê | Como usar |
|---|---|---|---|
| **Entrada** | `variable` | Parametrizar (description, type, default, validation, sensitive) | `var.nome` |
| **Saída** | `output` | Exportar valores depois do apply (IPs, IDs, ARN) | `terraform output` |
| **Locais** | `locals` | Constantes ou valores derivados, **imutáveis**, não fornecidos pelo usuário | `local.nome` (aula 5); o exemplo da aula 4 usa `locals.instanceType` |

**Tipos**: string, number, bool · list, map, set, object, tuple.

**Como passar valores**: `default` → `terraform.tfvars` ou `*.auto.tfvars` → linha de comando → `TF_VAR_` → entrada interativa.

**Boas práticas**: centralizar em `.tfvars` · `sensitive = true` para segredos · `description` · `default` sempre que possível · `validation`.

Detalhes: [[TF 04 - Variáveis e output]] · [[TF 05 - Data e locals]]
