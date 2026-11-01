---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [SoC, Separation of Concerns, Separação de Conceitos, Separação de preocupações, MVC]
---

# Separação de Conceitos (SoC)

*Separation of Concerns*: princípio básico da engenharia de software. **Modulariza a solução para que cada módulo resolva um único problema.**

- Separa o sistema em áreas, seções ou módulos que, combinados, atingem o objetivo principal (um software, uma página web, um hardware).
- Normalmente aparece em softwares de **grande porte** ou em projetos com **mais de uma linguagem**.

**Exemplo: MVC (Model View Controller)**
- **View**: apresenta os dados ao usuário.
- **Model**: processamento de dados (regras de negócio).
- **Controller**: intermédio entre View e Model.

O MVC mostra como o SoC ajuda a criar uma arquitetura **flexível, manutenível e sustentável**.

O SoC foi um dos princípios adotados por Alistair Cockburn para propor a [[Arquitetura Hexagonal]]. A "separação de preocupações" também é um dos pontos do [[Clean Architecture (livro)|Clean Architecture]] e uma das considerações da [[O que é Arquitetura de Software|arquitetura de software]].

Aparece em: [[ARQ 05 - Arquitetura Hexagonal]]
