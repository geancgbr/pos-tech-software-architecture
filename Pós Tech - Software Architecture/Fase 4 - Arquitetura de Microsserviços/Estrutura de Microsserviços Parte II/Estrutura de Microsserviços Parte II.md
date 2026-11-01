---
tags: [pos-tech/fase-4, microsservicos, indice]
disciplina: Estrutura de Microsserviços Parte II
fase: 4
aulas: 6
---

# Estrutura de Microsserviços Parte II

[[Fase 4 - Arquitetura de Microsserviços]] · Revisão → [[Revisão - Estrutura de Microsserviços Parte II]] · Parte 1 → [[Estrutura de Microsserviços]]

> [!note] Os PDFs não trazem nome de autor. Nas aulas 1 a 4, o serviço usado nos Hands On é o **Catálogo de Produtos**. Em várias aulas, o "O que vem por aí" e o resumo tratam de temas diferentes do texto do Saiba Mais; as notas indicam o que vem de cada parte.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[MS2 01 - Desenhando a lógica de negócios com microsserviços]] | High-level domain model, [[DAO e DTO\|DAO]], [[Arquitetura Hexagonal]] |
| 2 | [[MS2 02 - Aplicando a lógica de negócios no microsserviço]] | [[Offline Lock (Pessimista e Otimista)]], [[DAO e DTO\|DTO e ORM]], [[Agregado]] |
| 3 | [[MS2 03 - Testando microsserviços]] | [[TDD (Test-Driven Development)]], [[Teste de Carga e Teste de Estresse]], [[Apdex]] |
| 4 | [[MS2 04 - Testando microsserviços, parte 2]] | CI/CD, [[SonarQube]], SAST e DAST, [[BDD (Behavior-Driven Development)]] |
| 5 | [[MS2 05 - Realizando o deploy de microsserviços]] | [[Criptografia e mTLS]], [[Estratégias de Deployment]] |
| 6 | [[MS2 06 - Realizando o deploy de microsserviços, parte 2]] | Alertas, [[OpenTelemetry]], [[SLI, SLO e SLA]], [[Error Budget]] |

## Ligações com outras disciplinas
- **DDD (Fase 1)**: [[Agregado]], [[Contexto Delimitado]], [[Linguagem Ubíqua]] e [[Subdomínios]] reaparecem aplicados a microsserviços.
- **Qualidade de Software e Desenvolvimento Seguro (Fase 1)**: [[TDD (Test-Driven Development)|TDD]], [[BDD (Behavior-Driven Development)|BDD]], [[Teste de Carga e Teste de Estresse|testes de carga e de estresse]], [[SonarQube]] e [[Análise Estática de Código]].
- **Monitoramento e Acesso Avançado (Fase 3)**: [[Apdex]], [[SLI, SLO e SLA]], [[Error Budget]] e alertas ([[Monitors do Datadog]]).
- **Kubernetes e OpenTelemetry (Fase 2)**: o Rolling Update ([[ReplicaSet e Deployment]]), o [[OpenTelemetry]] e o Elasticsearch/Kibana ([[EFK (Elasticsearch, Fluentd e Kibana)]]).

## Dúvidas em aberto
- Aula 6: o título é "Realizando o deploy de microsserviços - Parte 2", mas a aula não trata de deploy: o conteúdo é observabilidade (instrumentação, ELK, alertas, OpenTelemetry, SLI/SLO, Error Budget).
- Aula 2: o PDF se chama "... - Parte 2", mas a aula 1 não se chama "Parte 1" e trata de outro tema.

## Material
PDFs em `~/Desktop/Estrutura de Microsserviços Parte II /` ("Estrutura de Microsserviços II - Aula 1.pdf" a "Aula 6.pdf").
