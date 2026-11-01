---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [TDD, Test-Driven Development, Desenvolvimento Orientado a Testes, Red-Green-Refactor]
---

# TDD (Test-Driven Development)

**Desenvolvimento Orientado a Testes**: metodologia que consiste em **escrever testes automatizados antes da implementação do código**. Segue um ciclo de repetição em 3 etapas.

| Etapa | O que fazer |
|---|---|
| 🔴 **Red** | Escrever um teste **para falhar**, descrevendo o comportamento esperado antes de implementar |
| 🟢 **Green** | Implementar o **código mínimo** necessário para o teste passar |
| 🔵 **Refactor** | Melhorar a qualidade e a legibilidade **sem mudar o comportamento**, e executar o teste novamente |

- O fluxo vale para cenários simples e complexos: garante o mínimo de cobertura, valida diferentes cenários e refina o código continuamente.
- **Benefícios**: maior confiabilidade do código, menos defeitos e maior capacidade de refatoração.
- Também é a primeira boa prática de [[Teste de Unidade|testes de unidade]]: escrever os testes antes do código.
- O [[BDD (Behavior-Driven Development)|BDD]] é apresentado como uma **evolução natural do TDD**.

## Na disciplina DevOps (Fase 2, aulas 1 e 3)
- Na CI, tudo começa quando o dev cria um teste que **falha em 100% das tentativas** e, aos poucos, escreve o código e reescreve o teste até ficar pronto.
- É **o único processo totalmente manual** da integração contínua: "a integração contínua começa com um teste manual".
- O TDD aplica os testes desde o início da construção do software (Humble, 2014). → [[DEV 03 - Testes automatizados com CI]] · [[Testes Contínuos]]

Exemplo completo (`IsAlphaString`): [[QS 03 - Aplicando TDD na prática]]

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
O teste é escrito **antes** do código. Ciclo: escrever o teste → executar (**deve falhar**) → código **mínimo** para passar → **refatorar**. Útil em microsserviços, testados de forma **independente**, e encaixa no **CI/CD**; exige investimento inicial, com retorno em menos bugs ([[MS2 03 - Testando microsserviços]]).
