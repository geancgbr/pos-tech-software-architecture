---
tags: [pos-tech/fase-4, microsservicos, resiliencia, revisao]
disciplina: Resiliência em Microsserviços
---

# Revisão - Resiliência em Microsserviços

[[Resiliência em Microsserviços]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- O que é resiliência?
> A capacidade de sistemas, processos e componentes suportarem uma ampla variedade de falhas, mantendo a operação total ou parcial. É um requisito crítico. → [[Resiliência]]

> [!question]- Defeito × erro × falha?
> Defeito: o software não opera conforme as especificações. Erro: comportamento inadequado que pode originar um defeito. Falha: a causa raiz do erro (design, implementação ou operação). Todo defeito é causado por um erro.

> [!question]- Quais os três tipos de defeitos, e como lidar com cada um?
> Inconsistentes (ex.: Byzantine Failures): protocolos de consenso como Paxos ou Raft. Consistentes: normalmente 2n+1 réplicas. Fail-stop: normalmente n+1 réplicas.

> [!question]- Resiliência e disponibilidade são a mesma coisa?
> Não. A disponibilidade mede solicitações com sucesso ou tempo funcional; a resiliência não é apenas um indicador, mas um conjunto de estratégias e mecanismos para manter a disponibilidade diante de falhas.

> [!question]- 1.000 requisições em 1 hora, 40 com erro: qual a taxa de erros?
> 4% de erros (96% atendidas).

> [!question]- Defina MTTF, MTTR e MTBF.
> MTTF: tempo médio antes de um problema. MTTR: tempo médio para recuperar (quanto menor, melhor). MTBF = MTTF + MTTR (quanto maior, mais confiável). Ex.: 900 h + 100 h = 1.000 h. → [[MTTF, MTTR e MTBF]]

> [!question]- Qual a "principal e mais simples" estratégia de resiliência segundo a aula?
> Distribuição e balanceamento de carga com escalabilidade horizontal (auto-scaling), com URLs de health check monitoradas pelos balanceadores.

## Aula 2 - Padrões
> [!question]- O que é idempotência, e como garanti-la?
> Executar a operação várias vezes com o mesmo resultado, sem duplicidade. Usa-se uma chave de idempotência (nos cabeçalhos HTTP ou como parâmetro), validada e registrada antes de processar. → [[Idempotência]]

> [!question]- Quais os tipos de timeout?
> Connection Timeout (criar a conexão), Read/Write Timeout (ler ou enviar dados) e Idle Timeout (fechar conexões paradas). → [[Timeout]]

> [!question]- Por que o retry exige idempotência? Quais as estratégias?
> Para repetir sem duplicidades ou inconsistências. Estratégias: imediatos em memória, assíncronos (ex.: 202 Accepted) e com backoff exponencial. → [[Retry e Backoff Exponencial]]

> [!question]- Quais os estados do Circuit Breaker?
> Fechado (fluxo normal), aberto (bloqueia por um tempo) e meio aberto (algumas requisições testam a recuperação). → [[Circuit Breaker]]

> [!question]- O que é o Bulkhead? Dê o exemplo da aula.
> Isola partes do sistema alocando recursos (threads, conexões) a grupos de operações. Ex.: threads para pagamentos e outras para cadastro. → [[Bulkhead]]

> [!question]- Rate Limiting × Throttling?
> Rate Limiting: limite de requisições por período (ex.: Token Bucket; 100 req/min). Throttling: ajusta dinamicamente a taxa conforme a carga, podendo retornar 429. → [[Rate Limiting e Throttling]]

> [!question]- Graceful Degradation × fallback?
> O Graceful Degradation é preventivo (mantém o essencial, ex.: feature toggles); o fallback age depois que o problema ocorreu. → [[Fallback e Graceful Degradation]]

> [!question]- O que é Failover? Exemplo?
> Redirecionar automaticamente o tráfego para instâncias redundantes. Ex.: o cluster de banco transfere do nó primário para o secundário. → [[Failover]]

## Aula 3 - Na prática
> [!question]- Quais as três etapas da idempotência em APIs?
> Gerar a Idempotency Key (geralmente pelo cliente, ex.: UUID, no cabeçalho), armazenar chave + resposta num repositório persistente e, numa repetição, retornar a resposta armazenada.

> [!question]- No exemplo em Go, o que acontece se o serviço não responder em 2 s?
> A operação é cancelada pelo `context.WithTimeout` e o sistema devolve 504 Gateway Timeout.

> [!question]- Para que serve o jitter?
> Para evitar que vários clientes falhem ao mesmo tempo e reiniciem as tentativas de forma sincronizada.

> [!question]- Por que o Resilience4j foi criado?
> Como alternativa leve e modular ao Netflix Hystrix (descontinuado em 2018), usando só os módulos necessários e aproveitando o Java 8+. → [[Resilience4j]]

> [!question]- Janela deslizante por contagem × por tempo?
> Contagem: número fixo de chamadas num array circular. Tempo: buckets por segundo com agregações parciais. Ambas usam Subtract-on-Evict.

> [!question]- O que faz o `failureRateThreshold`?
> Define a porcentagem de falhas que abre o circuito (ex.: 50.0 = metade das chamadas).

## Aula 4 - Service Mesh
> [!question]- O que é um Service Mesh?
> Uma camada de infraestrutura que gerencia a comunicação entre serviços, fora do código: roteamento, segurança, observabilidade e resiliência. → [[Service Mesh]]

> [!question]- Data Plane × Control Plane?
> Data Plane: proxies sidecar (geralmente Envoy) que executam em tempo real. Control Plane: gerencia e configura os sidecars (descoberta, configuração dinâmica, certificados, telemetria).

> [!question]- Como o Service Mesh faz Canary e A/B Testing?
> Canary: pequena porcentagem para a nova versão (ex.: 5%/95%), aumentando gradualmente. A/B: roteia grupos por cabeçalhos, cookies, sessão ou porcentagens. → [[Estratégias de Deployment]]

> [!question]- O que é Traffic Mirroring?
> Duplicar o tráfego real para a nova versão só para monitoramento, sem usar a resposta.

> [!question]- API Gateway × Service Mesh?
> O API Gateway atua na borda (tráfego externo); o Service Mesh permeia toda a malha interna.

> [!question]- Istio × Linkerd × Consul Connect?
> Istio: flexível e completo, curva íngreme. Linkerd: simples e performático (proxies em Rust). Consul Connect: HashiCorp, ambientes híbridos e multi-cloud.

## Aula 5 - Chaos Engineering
> [!question]- Como surgiu o Chaos Engineering?
> Na Netflix, na migração para a AWS (2008); o Chaos Monkey (Greg Orzell, 2010) encerrava instâncias EC2 aleatoriamente em produção. → [[Chaos Engineering]]

> [!question]- Quais os quatro princípios?
> Definir o estado estável, formular hipóteses, introduzir variáveis do mundo real e executar em produção (com progressão gradual).

> [!question]- Quais os critérios de uma boa hipótese?
> Específica, mensurável, alcançável, relevante e temporal.

> [!question]- Monitoramento × observabilidade?
> Monitoramento: métricas conhecidas e predefinidas. Observabilidade: entender o estado interno pelas saídas externas. O Chaos Engineering precisa dos dois.

> [!question]- Cite as ferramentas da aula.
> Chaos Toolkit (declarativo, plugins), Gremlin (comercial), Litmus (CRDs, GitOps) e Chaos Mesh (interface web).

## Pontos fracos
- 
