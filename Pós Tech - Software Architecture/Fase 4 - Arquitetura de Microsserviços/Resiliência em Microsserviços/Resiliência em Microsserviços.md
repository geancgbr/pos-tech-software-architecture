---
tags: [pos-tech/fase-4, microsservicos, resiliencia, indice]
disciplina: Resiliência em Microsserviços
fase: 4
aulas: 5
---

# Resiliência em Microsserviços

[[Fase 4 - Arquitetura de Microsserviços]] · Revisão → [[Revisão - Resiliência em Microsserviços]]

> [!note] Os PDFs não trazem nome de autor. A disciplina vai da teoria ([[Resiliência]], métricas, padrões) à prática em código (Python, Go, Node.js e [[Resilience4j]] em Java), depois à infraestrutura ([[Service Mesh]]) e por fim ao [[Chaos Engineering]].

## Aulas
| #   | Aula                                            | Conceitos-chave                                                                                                                                                                      |
| --- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | [[RES 01 - Introdução à resiliência]]           | [[Resiliência]] (defeito, erro e falha), [[MTTF, MTTR e MTBF]], balanceamento e health checks                                                                                        |
| 2   | [[RES 02 - Padrões de resiliência]]             | [[Idempotência]], [[Timeout]], [[Retry e Backoff Exponencial]], [[Circuit Breaker]], [[Bulkhead]], [[Rate Limiting e Throttling]], [[Fallback e Graceful Degradation]], [[Failover]] |
| 3   | [[RES 03 - Resiliência na prática]]             | Idempotency Key, `context.WithTimeout`, jitter, [[Resilience4j]], janelas deslizantes                                                                                                |
| 4   | [[RES 04 - Service Mesh e controle de tráfego]] | [[Service Mesh]] (Data e Control Plane), [[Sidecar]], Canary e A/B ([[Estratégias de Deployment]]), Istio, Linkerd, Consul Connect                                                   |
| 5   | [[RES 05 - Chaos Engineering]]                  | [[Chaos Engineering]] (Chaos Monkey, princípios, ferramentas), observabilidade                                                                                                       |

## Ligações com outras disciplinas
- **Estrutura de Microsserviços (Fase 4)**: o [[Circuit Breaker]] já aparecia na comunicação entre processos e no API Gateway; aqui ganha janelas deslizantes, Resilience4j e Service Mesh.
- **Estrutura de Microsserviços Parte II (Fase 4)**: [[Criptografia e mTLS]] e [[Estratégias de Deployment]] reaparecem no Service Mesh.
- **Arquitetura de Software (Fase 1)**: [[Disponibilidade e Observabilidade]] e [[Escalabilidade]].
- **Monitoramento (Fase 3)**: [[Sidecar]], [[SLI, SLO e SLA]], [[Error Budget]] e o [[API Gateway]] (na borda, enquanto o Service Mesh cobre a malha interna).
- **OpenTelemetry (Fase 2)**: [[Três Pilares da Observabilidade (Logs, Métricas e Traces)]] e o eBPF em [[Tendências da Observabilidade (eBPF, Profiling e AIOps)]].

## Dúvidas em aberto
- Aula 1: "defeito" = fault e "falha" = failure na lista, mas os títulos das seções trocam os termos.
- Aula 1 × aula 5: MTTR é "Mean Time to **Repair**" e depois "Mean Time To **Recovery**".
- Aula 2: *Release It!* é atribuído a Michael T. Nygard no texto e a "NORMAN, M." nas referências; a primeira figura é a Figura 2.
- Aula 3: a seção da janela por tempo repete "baseada em contagem"; os YAMLs de configuração estão só em imagem (Figuras 2 e 3); a numeração dos códigos pula o 3 na parte Java.
- Meio-aberto do Circuit Breaker: "algumas requisições" (aula 2), "uma chamada" (aula 3), "quantidade limitada" (aula 4).
- Aula 5: o "O que você viu" cita teoria dos jogos e resposta humana a crises, que não estão no texto; as figuras saltam da 3 para a 8.

## Material
PDFs em `~/Desktop/Resiliência em microservices /` ("Aula 01 - Introdução a resiliência.pdf" a "Aula 05 - Chaos Engineering.pdf").
