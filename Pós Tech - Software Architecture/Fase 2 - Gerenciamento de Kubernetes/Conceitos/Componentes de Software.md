---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Componentes, Componentização, Componente de software]
---

# Componentes de Software

**Unidades de código com responsabilidade bem definida**, agrupadas para resolver problemas. Fazem coisas simples com **total competência** e têm **interfaces de uso bem definidas e explícitas** (ex.: "abrir conexão", "rodar comando", "rodar pesquisa").

**Regras e conceitos**
- **Responsabilidade mínima**: o mínimo para ser útil num contexto; nada incompleto.
- **Isolamento**: cada componente com sua responsabilidade, **sem sobreposição**.
- **Composição e desacoplamento**: combinar componentes; mesmo que um componente seja acoplado por dentro, ele fica desacoplado do resto.
- **Usar o mínimo** e compor componentes existentes.
- **Adaptar a ferramenta à necessidade**, nunca "entortar" a arquitetura para caber num componente ou framework (o que gera débito técnico).
- **Conhecer arquiteturas diferentes**: prática e estudo de código aberto.

**Reutilização**: bibliotecas, repositórios de componentes, git/GitHub/GitLab, **npm** e **pip**. **Framework** é uma estrutura de código "pré-fabricada" (ex.: **Spring**, **Express**).

Alternativa: [[Arquitetura Monolítica]]. Na Fase 1, o tema aparece em [[Modularização]].

Aparece em: [[CA 06 - Componentes]]
