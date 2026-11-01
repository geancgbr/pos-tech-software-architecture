---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 7
fonte: "POSTECH - Aula7_rev2.pdf"
---

# TF 07 - Loops e expressões

← [[TF 06 - Módulos]] · [[Terraform]] · Próxima → [[TF 08 - Criação de infra com AWS]]

> [!summary] Em uma frase
> Os **[[Loops e Expressões no Terraform|loops]]** criam vários recursos sem repetir código. O **`count`** serve para "clones" (mesma configuração), e o **`for_each`**, para recursos com valores diferentes (lista ou mapa). As **expressões** são trechos que retornam valores.

## Hands On (vídeos)
Criar **três instâncias EC2** na AWS com um único bloco de EC2, usando loops e expressões.

## count
- A forma **mais simples** de loop, em recursos ou módulos. Define **quantas instâncias** criar, com um número fixo ou uma variável.
- **Exemplo da aula** (Figura 1): `count` cria **3 instâncias**. Mudando `instance_count`, muda a quantidade sem alterar a estrutura.
- Com `count`, o Terraform cria uma **lista de instâncias**, e cada uma é referenciada **pelo índice** (ex.: a lista de IPs no output, Figura 2).

## for_each
- **Mais flexível**: itera sobre **mapas ou listas** e cria um recurso **por item**. É ideal quando os valores **podem ser diferentes**.
- Usa **chave e valor** em vez de um número, associando cada recurso a uma **chave única**.

**Com lista**:
```hcl
variable "instances" {
  default = [
    "t2.micro",
    "t2.small",
    "t2.medium"
  ]
}

resource "aws_instance" "example" {
  for_each      = toset(var.instances)
  ami           = "ami-0453ec754f44f9a4a"
  instance_type = each.key
}
```

**Com mapa**:
```hcl
variable "instances" {
  default = {
    "web-server" = {
      ami           = "ami-0c55b159cbfafelf0",
      instance_type = "t2.micro"
    }
    "db-server" = {
      ami           = "ami-0a91cd140a1fc648b",
      instance_type = "t2.small"
    }
  }
}

resource "aws_instance" "example" {
  for_each      = var.instances
  ami           = each.value.ami
  instance_type = each.value.instance_type
}
```
**`each.key`** e **`each.value`** acessam a chave e o valor.

## count × for_each
| | count | for_each |
|---|---|---|
| Usa | Um **número inteiro** | **Mapas ou listas** |
| Ideal para | O **mesmo tipo de recurso várias vezes, com a mesma configuração** | Recursos com **atributos ou configurações diferentes** |

Os dois podem ser combinados com expressões condicionais e variáveis.

## Expressões
**Trechos de código que retornam um valor**, usados em variáveis, recursos, outputs e funções.

| Tipo | O que permite |
|---|---|
| **Atribuição de variáveis e constantes** | Receber valores diretamente ou calculados |
| **Aritméticas e comparações** | Soma, subtração, multiplicação, divisão, módulo; `==`, `!=`, `>`, `<`, `>=`, `<=` |
| **Concatenar strings** | Interpolação com **`${}`** |
| **Listas e mapas** | Acessar, adicionar, filtrar ou transformar dados |
| **Funções** | `length()`, `join()`, `lookup()`, `element()`, entre outras |

## Referências
HashiCorp: Manage similar resources with count, Create Dynamic Expressions, Manage similar resources with for_each
