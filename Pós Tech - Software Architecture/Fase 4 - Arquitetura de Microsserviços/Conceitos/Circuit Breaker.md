---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Disjuntor]
---

# Circuit Breaker

Padrão que **evita chamadas desnecessárias** a serviços **degradados**, para sistemas **resilientes e autorrecuperáveis**, mitigando a **lentidão propagada** e o **efeito cascata** ([[MS 02 - Comunicação entre processos com microsserviços]]).

| Estado | O que acontece |
|---|---|
| **Fechado** | Chamadas normais; acima de um limite de falhas (ex.: mais de 5 em 2 minutos) → **aberto** |
| **Aberto** | Interrompe todas as chamadas; depois de um tempo → **semi-aberto** |
| **Semi-aberto** | Deixa passar algumas chamadas: sucesso → **fechado**; falha → **aberto** |

- Os clientes **falham rápido**, sem esperar o timeout, e vão para cenários alternativos (erro, resultados parciais).
- O **API Gateway** pode implementá-lo por políticas ([[MS 03 - Gerenciando API com API Gateway e BFF]]).

## Na disciplina Resiliência em Microsserviços (Fase 4)
- Inspirado no disjuntor elétrico; bloqueia requisições com **alta taxa de erros**. Exemplo: API externa falhando. Prós: previne cascata, reduz latência, estabilidade. Contras: configurar limites, monitoramento contínuo. Implementações: **Resilience4j** ou **Hystrix** ([[RES 02 - Padrões de resiliência]]).
- No [[Resilience4j]]: **janela deslizante** por contagem (array circular, **Subtract-on-Evict**, O(1)) ou por tempo (**buckets**); `failureRateThreshold`, `waitDurationInOpenState`; **fallback**; combinar com [[Bulkhead]] ([[RES 03 - Resiliência na prática]]).
- No [[Service Mesh]]: configurado de forma **declarativa** no Control Plane (Istio ou Linkerd), sem alterar código; no meio-aberto, uma **quantidade limitada** de requisições de teste ([[RES 04 - Service Mesh e controle de tráfego]]).

> [!note] O meio-aberto permite "algumas requisições" ([[RES 02 - Padrões de resiliência]]), "uma chamada" ([[RES 03 - Resiliência na prática]]) e "uma quantidade limitada" ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[MS 02 - Comunicação entre processos com microsserviços]], [[MS 03 - Gerenciando API com API Gateway e BFF]], [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]], [[RES 04 - Service Mesh e controle de tráfego]]
