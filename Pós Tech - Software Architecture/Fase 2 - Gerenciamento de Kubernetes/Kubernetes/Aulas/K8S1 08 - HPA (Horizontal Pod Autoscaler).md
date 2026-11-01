---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 8
fonte: "Kubernetes/Aula 8.pdf (Thiago Adriano)"
---

# K8S1 08 - HPA (Horizontal Pod Autoscaler)

← [[K8S1 07 - Probes]] · [[Kubernetes]] · Próxima → [[K8S2 01 - Jobs e CronJobs]]

> [!summary] Em uma frase
> O **[[HPA (Horizontal Pod Autoscaler)|HPA]]** ajusta **automaticamente** o número de réplicas de um Pod com base nas **métricas de utilização de recursos** (CPU, memória, métricas personalizadas...), comparadas com **limites predefinidos**, entre um mínimo e um máximo de réplicas.

## Hands On
Exemplos práticos de como o HPA ajusta automaticamente a escala dos Pods com base na demanda de tráfego de um aplicativo.

## Como funciona
- Monitora as **métricas de utilização de recursos** dos Pods (como CPU e memória) e as compara com **limites predefinidos**.
  - Quando a utilização **ultrapassa** os limites → **aumenta** o número de réplicas.
  - Quando a utilização **diminui** → **diminui** o número de réplicas, para **economizar recursos**.
- Pode usar **CPU, memória e métricas personalizadas**. Também permite definir **limites de escala**: o número **mínimo e máximo** de réplicas.

**Benefícios**
- Os aplicativos são dimensionados **automaticamente conforme a demanda**, mantendo desempenho e disponibilidade em níveis aceitáveis.
- **Pode ajudar a reduzir os custos operacionais**, alocando recursos de maneira mais eficiente. Exemplo: com réplicas em excesso, diminui o número delas.

## Métricas suportadas
| Métrica | Base |
|---|---|
| **CPU** | A **mais comum**: a utilização de CPU pelos Pods |
| **Memória** | A utilização de memória pelos Pods |
| **Uso personalizado de métricas** | Definidas pelo usuário, com base em estatísticas do aplicativo ou indicadores de desempenho |
| **Medidas externas** | Fornecidas por sistemas de monitoramento de terceiros, como o **Prometheus** |
| **E/S de disco** | Em alguns casos, a E/S de disco de um Pod |

- Cada métrica tem vantagens e desvantagens, e a escolha depende do aplicativo e do ambiente. Exemplo: **CPU** para aplicativos que exigem muita CPU; **memória** para os que usam muita memória.

## Passo a passo do exemplo
1. **Criar um Deployment** (Figura 1): um Pod com um contêiner **nginx** e **1 réplica**.
2. **Criar o objeto HPA** para o Deployment (Figura 2): monitora a **CPU** e ajusta as réplicas **entre 1 e 10**, com objetivo de **70% de utilização de CPU**.
3. **Fazer um teste de carga** para aumentar o uso de CPU, com ferramentas como o **K6** ou o **JMeter**.
4. **Verificar** se o HPA aumentou as réplicas: `kubectl get hpa`.
5. **Reduzir a carga** e verificar se o HPA diminuiu as réplicas.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
