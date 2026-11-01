---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Recreate, Blue-Green Deployment, Blue-Green, Canary Release, Canary, Teste A/B, Shadow Deployment]
---

# Estratégias de Deployment

Formas de publicar os serviços em produção de maneira **segura e resiliente**, reduzindo o impacto nos usuários ([[MS2 05 - Realizando o deploy de microsserviços]]).

| Estratégia | Resumo |
|---|---|
| **Recreate** | Remove **todas** as instâncias antigas antes das novas; consistência; ideal se **tolera inatividade** |
| **Blue-Green** | **Blue** (atual) e **Green** (nova) em paralelo; alternar o tráfego por **balanceador**; reversão rápida |
| **Canary Release** | Liberação **gradual** para uma **porcentagem** de usuários; testar com usuários reais |
| **Rolling Update** | Substitui as instâncias **uma a uma ou em lotes**; ferramentas como o **Kubernetes** |
| **Teste A/B** | Divide o tráfego entre **duas versões** para **comparar** o desempenho (ex.: engajamento, taxas de conversão); **Beta Users** |
| **Shadow Deployment** | A nova versão recebe **cópia do tráfego real** sem ser exposta; NGINX, HAProxy ou **Istio** |

- O Rolling Update também aparece no Deployment do Kubernetes ([[ReplicaSet e Deployment]]).
- Os padrões de deployment **tradicional**, por **VM, container e serverless** são citados só no resumo da aula 5.

## Na disciplina Resiliência em Microsserviços (Fase 4)
Com o [[Service Mesh]] (ex.: Istio): **Canary** (ex.: 5% na v2 e 95% na v1, que o mesh **pode** reverter automaticamente ou notificar), **A/B Testing** (cabeçalhos, cookies, sessão ou porcentagens; ex.: 30%/70%) e **Traffic Mirroring** (cópia do tráfego real só para monitorar) ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[MS2 05 - Realizando o deploy de microsserviços]], [[RES 04 - Service Mesh e controle de tráfego]]
