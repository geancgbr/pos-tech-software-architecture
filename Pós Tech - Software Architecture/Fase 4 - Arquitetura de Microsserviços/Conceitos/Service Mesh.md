---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Malha de serviços, Data Plane, Control Plane, Istio, Linkerd, Consul Connect, Envoy]
---

# Service Mesh

**Camada de infraestrutura** dedicada à comunicação entre serviços, **fora do código** da aplicação: roteamento, segurança, observabilidade e resiliência de forma **transparente** ([[RES 04 - Service Mesh e controle de tráfego]]).

| | Data Plane | Control Plane |
|---|---|---|
| Papel | Executa em tempo real | Gerencia e configura os proxies |
| Componentes / funções | **Proxies sidecar** (geralmente **Envoy**): roteamento, balanceamento, telemetria, **mTLS**, resiliência | Descoberta de serviço, configuração dinâmica, certificados, telemetria agregada |

- Resolve **duplicação de código, acoplamento, observabilidade difícil e gerenciamento de falhas**.
- **Controle de tráfego**: Canary, A/B Testing, Load Balancing, Traffic Mirroring, roteamento por conteúdo, Fault Injection, timeouts e retries. Ver [[Estratégias de Deployment]].
- Aplica [[Circuit Breaker]], [[Retry e Backoff Exponencial|Retry]] e [[Timeout]] de forma **centralizada**, sem alterar o código (o Circuit Breaker, de forma **declarativa** no Control Plane).
- **API Gateway** na **borda**; Service Mesh em **toda a malha** interna.
- **Implementações**: **Istio** (Google, IBM e Lyft; Envoy; Pilot, Citadel, Galley, Mixer descontinuado; flexível, curva íngreme), **Linkerd** (Buoyant; proxies em Rust; simples e performático) e **Consul Connect** (HashiCorp; híbrido e multi-cloud).
- **Tendências**: Ambient Mesh (sem sidecars), **eBPF** (ex.: Cilium) e **WASM**.
- Na disciplina Estrutura de Microsserviços Parte II, o service mesh é citado junto com os chassis ([[MS2 05 - Realizando o deploy de microsserviços]]).

Aparece em: [[RES 04 - Service Mesh e controle de tráfego]], [[MS2 05 - Realizando o deploy de microsserviços]]
