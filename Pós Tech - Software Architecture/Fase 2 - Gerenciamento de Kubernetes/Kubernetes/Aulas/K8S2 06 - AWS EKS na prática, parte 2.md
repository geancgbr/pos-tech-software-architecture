---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 6
fonte: "Kubernetes parte 2/Aula 6.pdf (Thiago Adriano)"
---

# K8S2 06 - AWS EKS na prática, parte 2

← [[K8S2 05 - AWS EKS na prática, parte 1]] · [[Kubernetes]] · Próxima → [[K8S2 07 - Kubernetes CI-CD]]

> [!summary] Em uma frase
> A escalabilidade na prática com **Deployment + [[HPA (Horizontal Pod Autoscaler)|HPA]]** no EKS: o HPA responde **automaticamente** às mudanças na demanda de tráfego, **sem intervenção manual** de quem opera. A carga é simulada com o **K6**.

## Hands On
Configurar o HPA junto com o Deployment, ajustando o número de Pods em execução para diferentes níveis de demanda de tráfego.

## Por que o HPA
- Permite que o sistema **escale automaticamente** o número de Pods para atender à demanda, de forma inteligente e eficiente, **sem intervenção manual**.
- **Exemplo do e-commerce**: uma promoção gera um aumento repentino de tráfego.
  - **Sem o HPA**: a escala fica limitada às **configurações manuais**, com risco de **interrupções** e **atrasos nos pedidos**. A equipe teria de agir rápido, o que demanda tempo e é **propenso a erros humanos**.
  - **Com o HPA**: o número de Pods é ajustado automaticamente, garantindo **disponibilidade e qualidade** do serviço. Exemplo: se a demanda subir **50%**, o HPA pode ajustar os Pods para lidar com o aumento.

## Exemplo 1: HPA baseado em CPU
```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: my-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-deployment
  minReplicas: 2
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```
Escala o Deployment **"my-deployment"** mantendo a CPU em **50%**: se a utilização exceder esse limite, aumenta até **10** Pods; se diminuir, reduz até **2**.

## K6
- Ferramenta **de código aberto** para criar scripts de **teste de carga em JavaScript**. Suporta **HTTP, WebSocket e gRPC** e simula **usuários virtuais em larga escala** para testar picos de tráfego.
- Usos: testar **antes de lançar** para o público e **monitorar continuamente** o desempenho em produção, detectando problemas antes que afetem os usuários.
- Pode parecer complexo, mas é projetado para ser **fácil de usar**, com ampla documentação e comunidade ativa.

**Script de teste**
```javascript
import http from 'k6/http';
import { check } from 'k6';
import { Rate } from 'k6/metrics';

const failureRate = new Rate('check_failure_rate');

export default function () {
  const res = http.get('http://your-app.com');
  check(res, {
    'status is 200': (r) => r.status === 200,
  }) || failureRate.add(1);
}
```
Envia uma solicitação **GET** para a URL do aplicativo. Pode ser personalizado com testes adicionais, como **simulação de login** ou **envio de formulários**.

## Exemplo 2: Deployment + HPA
- **Deployment** `my-deployment`: **3 réplicas**, rótulo `app: my-app`, contêiner `my-container` com a imagem `my-image` na **porta 80** e `imagePullSecrets` com `my-registry-credentials`.
- **HPA** `my-hpa` (no mesmo arquivo, separado por `---`): `minReplicas: 1`, `maxReplicas: 10`, **`targetCPUUtilizationPercentage: 75`**. Mantém a CPU em **75%**, entre **1 e 10** Pods, conforme a demanda.

**Rodando o teste**
```bash
k6 run --vus 10 --duration 30s test.js
```
Executa o script com **10 usuários virtuais por 30 segundos**. O K6 gera **relatórios de métricas** que ajudam a identificar problemas e monitorar o desempenho durante o teste.

> [!note] Os blocos de código foram reindentados, porque a extração do PDF perdeu os recuos. Os valores são os do PDF.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
