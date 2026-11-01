---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Bibliotecas de terceiros, Dependências inseguras, Cryptojacking, Cryptominer, UA-Parser-JS, npm audit]
---

# Segurança de Bibliotecas de Terceiros

Importar bibliotecas **sem analisá-las** traz riscos de segurança e confiabilidade, principalmente quando não se controla o código de todas as dependências.

> [!example] UA-Parser-JS (2021)
> Pacote NPM com cerca de 24 milhões de downloads no mês. Três versões foram contaminadas com código para minerar a criptomoeda Monero (**cryptojacking**).

**Cryptominer**: script ou programa malicioso que usa a CPU ou a GPU para minerar criptomoedas **sem consentimento**. **Cryptojacking** é essa prática, que costuma causar lentidão e sobrecarga.

**Como se proteger** (aula 3)
- Fontes **confiáveis** (repositórios oficiais, desenvolvedores renomados).
- Bibliotecas **populares** (mais revisões e auditorias): veja os downloads e a comunidade.
- **Auditorias de código**, internas ou com especialistas.
- **Testes de segurança regulares**, incluindo as bibliotecas.
- Acompanhar as **vulnerabilidades conhecidas**, por exemplo com o **`npm audit`**.
- Manter **tudo atualizado**.
- **[[Análise Estática de Código]]**.

**Ferramenta do OWASP para isso** (aula 5): [[OWASP Dependency-Track]].

Aparece em: [[DS 03 - Bibliotecas de software]], [[DS 05 - OWASP e OWASP Top 10]]
