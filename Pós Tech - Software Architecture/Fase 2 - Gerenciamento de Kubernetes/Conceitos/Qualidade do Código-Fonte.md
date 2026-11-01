---
tags: [pos-tech/fase-2, devops, conceito]
aliases: [Qualidade do código, Code quality, Código legado, Quality Gates, Quality Profiles]
---

# Qualidade do Código-Fonte

Uma medida de **quão bem escrito, organizado, eficiente e confiável** é o código, e de como ele atende aos requisitos funcionais e não funcionais de forma eficaz e sustentável.

**Características**: legibilidade · eficiência · confiabilidade · escalabilidade · manutenibilidade · segurança.

**Como garantir no DevOps**: TDD e CI · análise estática (segurança, performance, legibilidade) · code review, pair programming e depuração conjunta · ferramentas de revisão na CI.

**Sinais de baixa qualidade**: duplicação · falta de coesão · complexidade · falta de documentação · falta de validação de entrada · ausência de testes automatizados · falta de otimização · variáveis confusas · falta de modularização (bloco monolítico) · condicionais demais · falta de tratamento de exceções.

**Limitações das ferramentas**: configuração incorreta · falso positivo · falso negativo · personalização limitada · demora · dependência de versão · uso incorreto dos dados.

**Código legado** (antigo, ainda em produção): integração difícil · detecção limitada · muitos problemas · restrições de tempo e orçamento (atualizar legado pode ser caro e demorado). A abordagem é estratégica e a modernização é **gradual**.

**Ferramentas**: SonarQube/SonarCloud · ESLint · PMD · Checkstyle · CodeSonar · ReSharper · FindBugs · PyLint. No Hands On, o SonarQube com **Quality Profiles** e **Quality Gates** integrado ao GitHub.

Na Fase 1: [[Análise Estática de Código]], [[SonarQube]], [[Manutenibilidade]].

Aparece em: [[DEV 04 - Qualidade do código-fonte]]
