---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [HPA, Horizontal Pod Autoscaler, HorizontalPodAutoscaler, Auto Scaling]
---

# HPA (Horizontal Pod Autoscaler)

Recurso do Kubernetes que **ajusta automaticamente** o número de réplicas de um Pod com base nas **métricas de utilização de recursos**, comparadas com **limites predefinidos**: quando a utilização ultrapassa esses limites, aumenta as réplicas; quando diminui, diminui as réplicas, para **economizar recursos**. Tem limites de escala (**mínimo e máximo** de réplicas).

- **Métricas**: **CPU** (a mais comum) · **memória** · **personalizadas** · **externas** (ex.: [[Prometheus]]) · **E/S de disco**.
- **Benefícios**: dimensionamento automático conforme a demanda; pode ajudar a **reduzir os custos operacionais**.
- **Por que no EKS** (parte 2): responde às mudanças de tráfego **sem intervenção manual**. Sem ele, a escala fica limitada às configurações manuais, com risco de interrupções e de erros humanos (exemplo da promoção num e-commerce).

| Exemplo | Mín. | Máx. | Alvo de CPU | Aula |
|---|---|---|---|---|
| HPA para um Deployment nginx | 1 | 10 | 70% | [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]] |
| `my-hpa` para `my-deployment` | 2 | 10 | 50% | [[K8S2 06 - AWS EKS na prática, parte 2]] |
| `my-hpa` junto com o Deployment | 1 | 10 | 75% | K8S2 06 |

- **Testando**: gerar carga com o **K6** ou o **JMeter** ([[Ferramentas de Teste de Carga (JMeter e K6)]]) e conferir com `kubectl get hpa`.
- Na parte 2, o YAML usa `apiVersion: autoscaling/v1`, `kind: HorizontalPodAutoscaler`, `scaleTargetRef` e `targetCPUUtilizationPercentage`.

Aparece em: [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]], [[K8S2 06 - AWS EKS na prática, parte 2]]
