---
tags: [pos-tech/fase-3, monitoramento, datadog, conceito]
aliases: [sidecars, Datadog Sidecar]
---

# Sidecar

Instrumentar uma aplicação **de forma desacoplada do mesmo host**, a partir de **outro servidor/container** ([[MAV 02 - Introdução APM Datadog]]).

- **Por quê**: instrumentação **transparente**, **sem usar os recursos da aplicação**, e garantia do **envio de erros**: se a aplicação ou o container "morrer", o erro ainda chega ao [[Datadog]].
- **Custo**: um pouco maior, com **um host exclusivo por aplicação**: cada container da aplicação sobe com outro container de sidecar.
- **Possibilidades**: monitoramento de aplicações (CPU, memória, latência de rede) · rastreamento distribuído · registro de logs · análise de erros · monitoramento de infraestrutura.
- Ver a Figura 1 do PDF (Datadog Sidecar with K8s).

## Na disciplina Resiliência em Microsserviços (Fase 4)
No [[Service Mesh]], o **Data Plane** é feito de **proxies sidecar** (geralmente **Envoy**) ao lado de cada instância, interceptando todo o tráfego de entrada e saída. O **Ambient Mesh** do Istio elimina a necessidade de sidecars para todos os serviços ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[MAV 02 - Introdução APM Datadog]], [[RES 04 - Service Mesh e controle de tráfego]]
