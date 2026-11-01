---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Probes, Liveness, Readiness, Startup, Liveness probe, Readiness probe, Startup probe]
---

# Probes do Kubernetes

Verificam a **saúde de um aplicativo** num Pod. São definidas no **manifesto do Pod** (YAML), com **tipo, caminho de solicitação e intervalos de verificação**. **Sem elas, os aplicativos podem falhar silenciosamente.**

| Probe | Verifica | Se falhar |
|---|---|---|
| **Liveness** | Se está **em execução** e respondendo | **Reinicia o Pod** |
| **Readiness** | Se está **pronto para receber solicitações** | **Remove do balanceador de carga** |
| **Startup** | Se está **sendo iniciado corretamente** | **Reinicia o Pod** |

- **Por padrão**, usam um **endpoint HTTP** com **GET**, esperando **200 OK**. A Liveness também pode ser **TCP** (porta específica) ou **Exec**.
- **Boas práticas**: usar as três · ajustar os intervalos · **endpoints diferentes por probe** · preferir as configurações padrão · usar as avançadas com cuidado · testar · monitorar com o **[[Prometheus]]** · documentar · monitorar as falhas.
- **Exemplo da aula**: Liveness a cada 10 s (espera máxima de 5 s) · Readiness a cada 5 s (3 s) · Startup com atraso inicial de 120 s, a cada 30 s (10 s).

Aparece em: [[K8S1 07 - Probes]]
