---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [count, for_each, each.key, each.value, Expressões no Terraform]
---

# Loops e Expressões no Terraform

| | `count` | `for_each` |
|---|---|---|
| Usa | Número inteiro (fixo ou variável) | **Lista** ou **mapa** (o exemplo usa `toset()`) |
| Referência | **Índice** (lista de instâncias) | **`each.key`** / **`each.value`** (chave única) |
| Ideal para | O **mesmo recurso várias vezes, com a mesma configuração** ("clones") | Recursos com **configurações diferentes** |

**Expressões**: trechos que **retornam valores**. Atribuição · aritmética (soma, subtração, multiplicação, divisão e módulo) e comparações (`== != > < >= <=`) · concatenação com `${}` · listas e mapas · funções (`length()`, `join()`, `lookup()`, `element()`).

Exemplos: [[TF 07 - Loops e expressões]]
