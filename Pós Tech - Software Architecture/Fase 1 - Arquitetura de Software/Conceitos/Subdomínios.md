---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Subdomínio, Subdomínio Principal, Subdomínio Genérico, Subdomínio de Suporte, Core Domain, Core Subdomain, Generic Subdomain, Supporting Subdomain]
---

# Subdomínios

Partes do [[Domínio]]. São de três tipos:

| Tipo | O que é | Característica segundo a apostila | Exemplo na escola |
|---|---|---|---|
| **Principal** | O que faz o negócio especial e o **diferencia** dos outros no mercado | É a resposta para "o que faz o negócio diferente dos outros?" | Aulas e metodologias |
| **Genérico** | Processos **comuns no mercado**, como portal da empresa, loja on-line ou autenticação | Naturalmente complexos, com lógica de negócio, mas **não diferenciam** o produto ou serviço | Criptografia dos dados |
| **Suporte** | **Apoia** e complementa o principal, sem vantagem estratégica | Lógica simples, geralmente **CRUD** | Gestão de dados de pais e alunos |

> [!important] Depende do contexto
> O que é um subdomínio genérico para um domínio pode não ser para outro. O mesmo subdomínio pode ser de um tipo para um negócio e de outro tipo para outro negócio.

## Como identificar
A apostila traz um fluxograma para identificar o tipo de subdomínio (Figura 1, pág. 7 do PDF da aula 1, fonte: vladikk.com). O texto do PDF não descreve as etapas do fluxograma, então consulte a figura no PDF. A sugestão da apostila é usar o fluxograma para inferir os subdomínios de vários negócios e comparar semelhanças entre eles.

## Outros exemplos da aula
| Empresa | Principal | Genérico | Suporte |
|---|---|---|---|
| Netflix | Vídeos | Faturamento | Cadastro de filmes e séries |
| Azul | Voos | Autenticação do portal | Cadastro de pessoas no portal |
| DHL | Serviços logísticos | Contabilidade | Integração com outros sistemas logísticos |

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
Segundo o resumo da aula 1, a aplicação é decomposta por **capacidades de negócio** e **subdomínios DDD** ([[MS2 01 - Desenhando a lógica de negócios com microsserviços]]).

Aparece em: [[DDD 01 - Introdução ao Domain-Driven Design]], [[MS2 01 - Desenhando a lógica de negócios com microsserviços]]
