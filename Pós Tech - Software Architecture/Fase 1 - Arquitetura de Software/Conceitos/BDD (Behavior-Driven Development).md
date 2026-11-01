---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [BDD, Behavior-Driven Development, Desenvolvimento Guiado por Comportamento, Gherkin, SpecFlow, Cucumber]
---

# BDD (Behavior-Driven Development)

**Desenvolvimento Guiado por Comportamento**: foca na **colaboração** entre devs, testadores e partes interessadas, para construir o software a partir de **comportamentos e requisitos de negócio claros**.

- É uma **evolução natural do [[TDD (Test-Driven Development)|TDD]]**: descreve o comportamento esperado numa linguagem fácil para todos e amplia o escopo dos testes de unidade para os testes de **aceitação e integração**, abordando o software como um todo.
- O comportamento é definido em **cenários de uso**.

**Princípios**: colaboração · [[Linguagem Ubíqua|linguagem ubíqua]] · testes como especificações (documentação executável) · feedback rápido.

**Boas práticas**: identificar os cenários de uso · escrever os cenários de teste (entradas, ações, saídas) · automatizar · integração contínua · envolver as partes interessadas.

**Cenários do exemplo do hotel**: escritos com **Dado** · **Quando** · **E** · **Então**. Cada cenário descreve um comportamento específico a verificar.

**Ferramentas**: **SpecFlow** (.NET), que permite escrever cenários de teste em linguagem natural, como o **Gherkin**, e executá-los de forma automatizada, e **Cucumber** (várias linguagens).

Exemplos completos: [[QS 05 - Trabalhando com BDD]]

Também foi citado no Hands On da aula 3 de Arquitetura de Software: [[ARQ 03 - Documentação, testabilidade e modificabilidade]].

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
Estende o **TDD** com foco em **comportamento** e **colaboração** ("O que o sistema deve realizar?"). Cenários **frequentemente** em **Gherkin** (**Given**, **When**, **Then**), executados por **Cucumber, JBehave ou SpecFlow**, que **podem ser** incorporados ao **CI/CD**. Desafio: **manutenção** dos cenários ([[MS2 04 - Testando microsserviços, parte 2]]).
