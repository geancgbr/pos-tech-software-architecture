---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [HCL, HashiCorp Configuration Language]
---

# HCL (HashiCorp Configuration Language)

A linguagem de configuração da HashiCorp, usada no **Terraform, Nomad e Consul**. É **declarativa, legível por humanos e fácil de interpretar por máquinas**, e suporta expressões, variáveis, loops e condicionais.

**Características**: legibilidade (próxima de JSON e YAML, declarando o estado desejado) · **declarativo** (o quê, não como) · extensível e estruturado (blocos, atributos, argumentos, expressões, condicionais, interpolação) · **conversível para JSON**.

**Elementos**: **blocos** (`resource "<tipo_de_recurso>" "<identificador>"`) · **atributos e argumentos** (`name`, `role_arn`) · **sub-blocos** (`vpc_config`, `access_config`) · **variáveis** (`var.nome`) · **interpolação** (`"${var.subnetA}"`) · **condicionais e funções** (`[for s in ... : s.id if ...]`).

Exemplos: [[TF 01 - Introdução ao Terraform#Elementos do HCL]]
