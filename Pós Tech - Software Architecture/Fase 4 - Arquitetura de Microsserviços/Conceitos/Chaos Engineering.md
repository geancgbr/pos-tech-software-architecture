---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Engenharia do Caos, Chaos Monkey, Simian Army, Chaos Toolkit, Gremlin, Litmus, Chaos Mesh]
---

# Chaos Engineering

"Quebrar coisas de propósito", de forma **controlada**, para tornar os sistemas resilientes; uma **disciplina científica**, não falhas aleatórias ([[RES 05 - Chaos Engineering]]).

- **Origem**: Netflix, migração para a **AWS** (2008); **Chaos Monkey** de **Greg Orzell** (2010), que encerrava instâncias EC2 em produção no horário comercial; **Simian Army** (Latency, Conformity e Security Monkey).
- **Princípios**: estado estável · hipóteses · variáveis do mundo real · experimentos em **produção**, com progressão gradual.
- **Metodologia**: pergunta → hipótese (específica, mensurável, alcançável, relevante e temporal) → design (critérios de parada) → execução controlada → análise → melhoria.
- **Tipos**: infraestrutura, aplicação, dependências e segurança.
- **Ferramentas**: Chaos Toolkit (JSON/YAML, plugins), Gremlin (comercial), Litmus (CRDs, GitOps) e Chaos Mesh (interface web).
- Depende de **monitoramento e observabilidade**; métricas de sucesso: MTBF, MTTR, SLOs e Error Budget.
- Na aula 1, aparece como prática do mindset de resiliência ([[RES 01 - Introdução à resiliência]]); a **Fault Injection** do Service Mesh é uma prática essencial dele ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[RES 01 - Introdução à resiliência]], [[RES 04 - Service Mesh e controle de tráfego]], [[RES 05 - Chaos Engineering]]
