---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Análise estática, Static Analysis, SAST, ESLint, Pylint, RuboCop, Checkstyle, Cppcheck]
---

# Análise Estática de Código

**Processo automatizado** que examina o código-fonte **sem executá-lo**, procurando problemas potenciais, **vulnerabilidades de segurança**, erros de codificação e oportunidades de otimização.

| | Análise estática | Testes dinâmicos |
|---|---|---|
| Código | **Em repouso**, não é executado | **Executado** e testado em tempo real |
| Quando acha o problema | **Antes** de o programa rodar | Durante a execução |

**Abordagens**: léxica e sintática · fluxo de controle · dependências · segurança (SQL Injection, XSS) · estilo de código.

**Ferramentas**: **ESLint** (JavaScript) · **Pylint** (Python) · **RuboCop** (Ruby) · **Checkstyle** (Java) · **Cppcheck** (C/C++, inclusive vazamentos de memória) · **[[SonarQube]]** (várias linguagens, CI/CD).

Na disciplina Desenvolvimento Seguro (Fase 1, aula 3), aparece como estratégia para validar a segurança de bibliotecas ([[Segurança de Bibliotecas de Terceiros]]).

## Na disciplina DevOps (Fase 2, aula 4)
As ferramentas de análise estática avaliam a qualidade do código e identificam problemas de **segurança, performance e legibilidade**. Entre as plataformas de análise estática, a aula cita **SonarQube/SonarCloud, CodeSonar e FindBugs**; também lista outras ferramentas de qualidade de código, como **PMD** e o **ReSharper** (extensão do Visual Studio). As limitações (falso positivo, falso negativo etc.) e os desafios com código legado estão em [[Qualidade do Código-Fonte]].


## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
- **Linters**: análise estática de erros, bugs e padrões inconsistentes, que **podem ser configurados** para seguir um **guia de estilo**; muitos corrigem sozinhos. A **análise de qualidade de código** como um todo usa métricas como **complexidade ciclomática**, **débito técnico** e **cobertura de testes**.
- **SAST** (analisa o código sem executar) × **DAST** (analisa o app em execução, simulando ataques), integráveis ao CI/CD (ex.: **Fortify**) ([[MS2 04 - Testando microsserviços, parte 2]]).

Aparece em: [[DS 03 - Bibliotecas de software]], [[DS 04 - Análise estática de código]], [[MS2 04 - Testando microsserviços, parte 2]]
