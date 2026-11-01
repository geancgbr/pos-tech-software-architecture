---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Sonar]
---

# SonarQube

Plataforma de **[[Análise Estática de Código|análise estática]]** amplamente usada na indústria.

- **Várias linguagens**: Java, C#, JavaScript, Python, entre outras. Por isso é versátil para equipes com tecnologias diferentes.
- **Destaque**: visão **abrangente e detalhada** da qualidade do código. Identifica problemas, inconsistências, **vulnerabilidades de segurança** e oportunidades de otimização **antes** que virem bugs em produção.
- **Altamente integrável a CI/CD**: as análises são automatizadas no pipeline, com correção contínua, do desenvolvimento à entrega.
- No Hands On: integrado a uma pipeline, avaliando **métricas de cobertura** e vulnerabilidades.

## Na disciplina DevOps (Fase 2, aula 4)
O SonarQube (e o **SonarCloud**) aparece entre as ferramentas de qualidade de código. No Hands On, ele é integrado ao pipeline DevOps com a criação de **Quality Profiles** e **Quality Gates**, sincronizados com a esteira do GitHub. → [[DEV 04 - Qualidade do código-fonte]]

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
Usado na **inspeção contínua** da qualidade, com relatórios e sugestões de correção; **pode ser integrado** ao **CI/CD**, com verificação a cada commit ([[MS2 04 - Testando microsserviços, parte 2]]).

Aparece em: [[DS 04 - Análise estática de código]], [[MS2 04 - Testando microsserviços, parte 2]]
