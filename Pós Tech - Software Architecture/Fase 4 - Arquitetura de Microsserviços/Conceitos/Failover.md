---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Failover Pattern]
---

# Failover

Redireciona **automaticamente** o tráfego para instâncias ou serviços **redundantes** em caso de falha; comum em **balanceadores** e **clusters de banco**. **AWS** e **Google Cloud** oferecem soluções integradas ([[RES 02 - Padrões de resiliência]]).

- Exemplo: o cluster detecta a falha do **nó primário** e transfere para o **secundário**.
- Na aula 1, aparece como prática de **redundância** ([[RES 01 - Introdução à resiliência]]); no Hands On da aula 4, políticas de failover com **Istio** ([[RES 04 - Service Mesh e controle de tráfego]]); numa hipótese de Chaos Engineering, failover em menos de 10 s ([[RES 05 - Chaos Engineering]]).

Aparece em: [[RES 01 - Introdução à resiliência]], [[RES 02 - Padrões de resiliência]], [[RES 04 - Service Mesh e controle de tráfego]], [[RES 05 - Chaos Engineering]]
