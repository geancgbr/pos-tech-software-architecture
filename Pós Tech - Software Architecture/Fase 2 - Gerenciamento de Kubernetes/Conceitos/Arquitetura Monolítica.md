---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Monolito, Monólito, Monolítica]
---

# Arquitetura Monolítica

**Centraliza numa única unidade de código todas as responsabilidades** do software (interface com o usuário, acesso a recursos externos, regras de negócio, configurações): um "super software" altamente integrado (aula 6).

- **Não é intrinsecamente ruim**. Serve para soluções **pequenas**, com poucas interfaces, ou para um caso de uso muito específico, como **software embarcado** em micro e nanodispositivos.
- **Vira problema** quando junta muitas responsabilidades num componente, ou centraliza tudo em poucos componentes. A manutenção fica difícil, e o **custo cresce com o tempo de vida**.
- Na aula 7, o "Monólito" (Figura 1) tem as regras de negócio espalhadas pelos componentes, ao contrário dos **componentes isolados** da Arquitetura Limpa.

Outras disciplinas: em DDD, há casos em que o **kernel compartilhado** é inevitável, como em sistemas legados (a apostila cita os monólitos), enquanto se moderniza a solução ([[Padrões de Integração entre Contextos]]), e microsserviços × monolito é um exemplo de decisão para registrar numa [[ADR (Architecture Decision Record)|ADR]].

## Na disciplina Data Engineering (Fase 4)
A **Netflix** começou a adotar microsserviços (por volta de **2011**) porque a **arquitetura monolítica** não bastava para seu crescimento. A modelagem de bancos em microsserviços é **bastante diferente** da tradicional num monolito ([[DE 07 - Bancos de dados e microsserviços]]).

## Na disciplina Estrutura de Microsserviços (Fase 4)
- Um **único componente executável** (`.exe`, `.war`): módulos no **mesmo processo**, compartilhando **classes e banco** ([[MS 01 - Estratégias e padrões de microsserviços]]).
- **Vantagens enquanto pequena**: simples de desenvolver, testar e publicar; grandes mudanças fáceis; fácil de escalar (artefato em várias máquinas + balanceador).
- **Desafios ao crescer**: o PDF diz que o time-to-market **diminui** (e que isso reduz a competitividade, embora nos benefícios dos microsserviços "reduzir o time-to-market" seja positivo), menos autonomia das squads, merges, complexidade, IDE lenta, escala cara (máquinas de uso geral), menor confiabilidade (uma exceção derruba tudo) e **stack obsoleta**. Mais afetados: **manutenção, extensibilidade e testabilidade**.
- Uma decomposição errada em serviços gera um **monolito distribuído**.

Aparece em: [[CA 06 - Componentes]], [[CA 07 - Detalhes - dados, acesso e frameworks]], [[DE 07 - Bancos de dados e microsserviços]], [[MS 01 - Estratégias e padrões de microsserviços]]
