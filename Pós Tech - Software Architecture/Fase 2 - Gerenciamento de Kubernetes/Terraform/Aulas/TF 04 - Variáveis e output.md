---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 4
fonte: "POSTECH - Aula4_rev2.pdf"
---

# TF 04 - Variáveis e output

← [[TF 03 - Principais comandos]] · [[Terraform]] · Próxima → [[TF 05 - Data e locals]]

> [!summary] Em uma frase
> As [[Variáveis, Outputs e Locals no Terraform|variáveis]] parametrizam a IaC e evitam hardcoding. Há três tipos: **de entrada** (`variable`), **de saída** (`output`) e **locais** (`locals`). Os valores podem vir de default, `.tfvars`, linha de comando, `TF_VAR_` ou entrada interativa, com **validação** e **sensitive**.

## Hands On (vídeos)
Criar variáveis e um arquivo de **output**, para registrar e exibir informações dos recursos depois de criados na nuvem.

## Por que variáveis
**Placeholders** para valores definidos de fora ou no código. Deixam a configuração:
- **mais reutilizável**: vários ambientes (dev, produção) com o mesmo código;
- **mais fácil de gerenciar**: mudanças centralizadas;
- **mais segura**: informações sensíveis gerenciadas de fora.

## Os três tipos
**1. Variáveis de entrada (input variables)**, com o bloco `variable`:
```hcl
variable "regionDefault" {
  description = "Região usada para criação"
  type        = string
  default     = "us-east-1"
}

provider "aws" {
  region = var.regionDefault
}
```
- `description`: descrição opcional. `type`: o tipo (string, number, bool, list, map...). `default`: o valor padrão; **sem ele, o valor deve ser informado na execução**.
- Segundo a apostila, **todos esses parâmetros são opcionais**.
- Para usar: **`var.nome-var`**.

**2. Variáveis de saída (output variables)**: exportam valores gerados depois do apply (IP de uma instância, IDs).
```hcl
output "bucket_arn" {
  value = aws_s3_bucket.backend-tf.arn
}
```

**3. Variáveis locais (locals)**: valores intermediários ou constantes reutilizados no código, **não fornecidos pelo usuário**.
```hcl
locals {
  instanceType = "t2.micro"
  tags = {
    environment = "production"
    owner       = "team"
  }
}
```
No exemplo de uso da apostila, um `aws_eks_node_group` usa `instance_types = locals.instanceType`.

> [!warning] `locals.` × `local.`
> Nesta aula, o exemplo referencia o valor como **`locals.instanceType`**. Na aula 5, a apostila diz que um local é acessado pelo prefixo **`local`** (ex.: `local.key`, `local.tags`).

## Tipos de dados
| Simples | Complexos |
|---|---|
| **string** (texto) · **number** · **bool** (true/false) | **list** (lista ordenada) · **map** (pares chave-valor) · **set** (não ordenado, valores únicos) · **object** (propriedades nomeadas com tipos) · **tuple** (lista ordenada de tipos diferentes) |

```hcl
variable "tags" {
  type = map(string)
  default = {
    environment = "dev"
    owner       = "fiap"
    year        = "2024"
    squad       = "fiap-jedi"
  }
}
```

## Como fornecer valores
Na ordem de usabilidade da apostila:
1. **Valores padrão**: o `default`, que pode ser **sobrescrito** pelas outras formas.
2. **Arquivos `.tfvars`**: o Terraform busca automaticamente **`terraform.tfvars`** e **`*.auto.tfvars`** (o PDF grafa "Terraform.tfvars", com maiúscula, como faz com "Terraform" em todo o texto). São parecidos com um `.env` (chave=valor).
3. **Linha de comando**: sobrescreve o default (Figura 1 do PDF).
4. **Variáveis de ambiente**: com o prefixo **`TF_VAR_`** (Figura 2).
5. **Interatividade**: se não houver default nem outro valor, o Terraform **pede o valor** (Figura 3).

## Validação e variáveis sensíveis
```hcl
variable "instanceType" {
  default = "t2.micro"
  validation {
    condition     = contains(["t2.micro", "t3.micro"], var.instanceType)
    error_message = "Tipo de instancia invalido, escolha entre t2.micro ou t3.micro"
  }
}

variable "datadog_api_key" {
  type        = string
  sensitive   = true
  description = "Chave de API para o datadog"
}
```
**`sensitive = true`** evita que senhas e chaves apareçam em logs ou na saída.

## Boas práticas
- **Centralize** em arquivos `.tfvars`.
- **Marque o que é sensível.**
- **Documente** com `description`.
- **Use padrões** (`default`) sempre que possível.
- **Valide os valores.**

## Referências
HashiCorp: Variables, Sensitive Variables, Outputs
