---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [JMeter, K6]
---

# Ferramentas de Teste de Carga (JMeter e K6)

As duas mais conhecidas na comunidade. Têm funcionalidades semelhantes, mas diferem em **arquitetura, recursos e usabilidade**.

| | JMeter | K6 |
|---|---|---|
| O que é | Código aberto, em **Java**. Simula diferentes cenários de carga | Código aberto, para testes de carga e performance |
| Destaque | Centenas ou milhares de **usuários virtuais** executando ações num período | **Consumo mínimo de recursos**, alto desempenho. Testes de **pico, estresse e absorção** em pré-produção e controle de qualidade |
| Como começar | Baixar pelo GitHub, descompactar e executar o arquivo do SO em `\bin\` | `brew install k6` (macOS), `dnf` (Linux), Chocolatey ou instalador (Windows). Escrever um `index.js` e rodar `k6 run index.js` |
| Pré-requisitos | Não citados | JavaScript básico e VS Code |

Código do primeiro teste com K6: [[QS 06 - Testes de carga#Ferramentas]]

## Na disciplina Kubernetes (Fase 2)
- O **K6** e o **JMeter** aparecem como ferramentas para gerar carga e testar o [[HPA (Horizontal Pod Autoscaler)|HPA]] ([[K8S1 08 - HPA (Horizontal Pod Autoscaler)]]). Na parte 1, aula 5, os professores usaram o K6 para testar a escala com ReplicaSets e Deployments.
- **Parte 2, aula 6**: o K6 é descrito como ferramenta **de código aberto** para scripts de teste de carga em **JavaScript**, com suporte a **HTTP, WebSocket e gRPC** e **usuários virtuais em larga escala**. Serve para testar antes do lançamento e para **monitorar continuamente** em produção. Exemplo: `k6 run --vus 10 --duration 30s test.js` (10 usuários virtuais por 30 s). → [[K8S2 06 - AWS EKS na prática, parte 2]]

Aparece em: [[QS 06 - Testes de carga]], [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]], [[K8S2 06 - AWS EKS na prática, parte 2]]
