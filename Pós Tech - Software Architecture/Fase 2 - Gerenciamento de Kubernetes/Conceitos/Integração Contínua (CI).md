---
tags: [pos-tech/fase-2, devops, conceito]
aliases: [Integração Contínua, CI, Continuous Integration]
---

# Integração Contínua (CI)

Técnica em que os devs colocam o código num **único repositório**, para eliminar problemas e retrabalho e facilitar a localização de erros (Pires, 2019). Vem do **Extreme Programming** (Kent Beck, 1996) ([[Extreme Programming (XP)]]).

- **Regra do XP**: cada dev integra seu código **ao menos uma vez por dia**.
- **Objetivo**: além de otimizar os processos manuais (como os do Quadro 1: integração, build, testes e deploy, suscetíveis a erros), **propor a automatização de parte do desenvolvimento**, para que os processos rodem independentemente da vontade do dev (Kim et al., 2018).
- **Paul Duvall**: a CI é a **peça central do desenvolvimento**, porque garante a integridade com **um build a cada mudança**.
- **Valores** (Duvall, Matyas e Glover): reduzir riscos · reduzir processos manuais repetitivos · gerar software implantável a qualquer momento · dar visibilidade ao projeto · dar confiança no software.
- **Testes**: a CI precisa de testes executados constantemente, sem deixar erros corrigidos voltarem, com a qualidade da nova versão pelo menos igual à anterior. Ela "começa com um teste manual" (o TDD) ([[Testes Contínuos]]).
- Empresas ainda usam o modelo manual por **não estarem amadurecidas** para testes efetivos e automatizados.

Na Fase 1 (Qualidade de Software, aula 4), a "integração contínua" aparece como **estratégia de teste de integração** ([[Teste de Integração]]).

## Na disciplina GitHub Actions (aula 1)
- Os devs combinam regularmente as alterações num **repositório central**; depois disso, **compilações são criadas e testes são executados**.
- Tem um **componente de automação** (ferramenta de CI ou serviço de compilação) e um **componente cultural** (a mentalidade de integrar com frequência).
- **Objetivos**: detectar e resolver bugs mais rápido, melhorar a qualidade e reduzir o tempo para validar e lançar atualizações.
- **Antes**: os devs trabalhavam isolados por longos períodos, com merges complexos e erros acumulados. **Hoje**: confirmações frequentes num repositório compartilhado, com um controle de versão como o Git, testes de unidade locais antes de cada confirmação e um serviço de CI que roda os testes automaticamente.

## Na disciplina Kubernetes (parte 2, aula 7)
**CI** é o processo de **integrar as alterações do código ao projeto principal com frequência**, geralmente **várias vezes ao dia**, para detectar e corrigir problemas antes que fiquem maiores. O exemplo de YAML ("Node.js CI") roda a cada push na `main`: checkout, `npm install` e `npm test`. → [[K8S2 07 - Kubernetes CI-CD]]

Aparece em: [[DEV 01 - CI-CD principais conceitos]], [[GHA 01 - Introdução]], [[DEV 03 - Testes automatizados com CI]], [[K8S2 07 - Kubernetes CI-CD]]
