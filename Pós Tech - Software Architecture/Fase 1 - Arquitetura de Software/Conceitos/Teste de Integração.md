---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [Testes de integração, Integration Test, Top-Down, Bottom-Up, Sandwich, Big Bang]
---

# Teste de Integração

Valida a **interação entre componentes ou módulos**: garante que partes testadas individualmente funcionem **corretamente em conjunto**. Testar cada parte isoladamente (testes unitários) não garante isso.

**Problemas que encontra**: incompatibilidades entre componentes, erros de comunicação, falhas na passagem de dados.

**Passos**: ambiente controlado e semelhante ao de produção (bancos, serviços externos, APIs; Docker ajuda) → cenários realistas → execução automatizada e análise dos resultados.

## Estratégias
- **Top-Down**: dos módulos externos para os internos. Os externos são simulados ou usam **stubs**.
- **Bottom-Up**: dos módulos internos (baixo nível) para os superiores. As dependências externas são simuladas ou usam **mock objects**.
- **Sandwich** (híbrida): top-down e bottom-up ao mesmo tempo, integrando de forma centralizada.
- **Big Bang**: tudo de uma vez, sem abordagem incremental. Útil com poucos módulos ou módulos independentes.
- **Integração contínua**: integra e testa continuamente, à medida que novos módulos entram.

## Validações
Interface · Dados · Fluxo de controle · Comportamento · Desempenho. A descrição de cada uma está em [[QS 04 - Testes de integração#Tipos de validação]].

## Quem faz
Equipe de teste · especialistas em desenvolvimento · equipe de qualidade (QA, que faz a intermediação entre devs e testes). O essencial é a **colaboração**.

Na aula 1, o teste de integração aparece como um tipo de [[Teste de Caixa Branca e Caixa Preta|caixa branca]].

Aparece em: [[QS 01 - Principais conceitos]], [[QS 04 - Testes de integração]]
