---
tags: [pos-tech/fase-4, resiliencia, microsservicos, service-mesh, aula]
disciplina: Resiliência em Microsserviços
aula: 4
fonte: "Resiliência em microservices/Aula 04 - Service Mesh e Controle de Tráfego.pdf"
---

# RES 04 - Service Mesh e controle de tráfego

← [[RES 03 - Resiliência na prática]] · [[Resiliência em Microsserviços]] · Próxima → [[RES 05 - Chaos Engineering]]

> [!summary] Em uma frase
> O **Service Mesh** é uma **camada de infraestrutura** dedicada à comunicação entre serviços, **fora do código da aplicação**: o **Data Plane** (proxies **sidecar**, geralmente **Envoy**) executa e o **Control Plane** orquestra. Ele permite **controle de tráfego** (Canary, A/B, balanceamento, Traffic Mirroring, Fault Injection) e aplica **Circuit Breaker, Retry e Timeout** de forma **centralizada**, sem alterar o código. Implementações: **Istio, Linkerd e Consul Connect**; tendências: **Ambient Mesh, eBPF e WASM**. Ver [[Service Mesh]].

## Hands On (vídeos)
Nas videoaulas: como o **Istio** simplifica **Canary Deployments, testes A/B e políticas de failover** de forma centralizada e **sem alterar o código**; rollouts graduais, **rollbacks rápidos** e ajustes dinâmicos de tráfego; como os padrões de resiliência evitam falhas em cascata; e a **observabilidade** integrada (métricas, logs e traces).

## O que é e por que precisamos
- Analogia: numa festa em que todos falam ao mesmo tempo, o Service Mesh é o **organizador**.
- **Camada de infraestrutura** que gerencia a comunicação entre serviços: **não faz parte do código**; cuida de **roteamento, segurança, observabilidade e resiliência**, de forma **transparente** para quem desenvolve, que foca na **lógica de negócio**.
- Antes dele, essas funções ficavam **dentro de cada microsserviço**, em bibliotecas ou frameworks, o que gerava:

| Problema | O que o PDF diz |
|---|---|
| **Duplicação de código** | Cada serviço implementava retentativas, circuit breaker, logging etc. |
| **Acoplamento** | Dependência de bibliotecas específicas dificultava trocar de tecnologia |
| **Observabilidade difícil** | Visão centralizada do tráfego era um grande desafio |
| **Gerenciamento de falhas** | Diagnóstico complexo, com a lógica distribuída pela aplicação |

## Data Plane e Control Plane
| | **Data Plane** (o "músculo") | **Control Plane** (o "cérebro") |
|---|---|---|
| Papel | Executa as operações **em tempo real** | **Não manipula o tráfego**: gerencia e configura os sidecars; nele se definem **políticas, regras de roteamento e segurança** |
| Composição / funções | **Proxies sidecar** ao lado de cada instância, **geralmente** baseados em **Envoy**. Os serviços enviam as requisições ao **seu sidecar**, que encaminha ao **sidecar do destino**. Funções: **roteamento** · **balanceamento de carga** · **telemetria** (latência, taxa de erros, volume, logs e traces) · **segurança** (**mTLS**) · **resiliência** (Circuit Breaker, Retries, Timeouts) | **Descoberta de serviço** (registro de serviços e instâncias) · **configuração dinâmica** (distribui regras em tempo real) · **gerenciamento de certificados** para mTLS · **coleta e agregação de telemetria** |
| Figuras | Figura 1 (TechTarget: sidecar proxy) | Figura 2 (TargetSo) e Figura 3 (Medium) |

- Essa separação torna o Service Mesh **escalável e flexível**: novas funcionalidades de rede **sem modificar o código**. Ver [[Sidecar]], [[Criptografia e mTLS]] e [[Descoberta de Serviços]].

## Controle de tráfego
Vai além do balanceamento simples, permitindo estratégias avançadas de **deployment e testes**. Ver [[Estratégias de Deployment]].

| Técnica | Como funciona com o Service Mesh |
|---|---|
| **Canary Deployment** (Figura 4) | Uma **pequena porcentagem** do tráfego vai para a nova versão (o "canário"); se for bem, aumenta-se **gradualmente**. Com o **Istio**, ex.: **5%** para a v2 e **95%** na v1; se a v2 tiver problemas (erros, latência), o mesh **pode reverter automaticamente** para a v1 ou **notificar** os operadores |
| **A/B Testing** (Figura 5) | Compara **duas versões** para ver qual desempenha melhor (ex.: duas interfaces, engajamento). Roteia grupos de usuários **sem que percebam**, por **cabeçalhos HTTP, cookies, atributos de sessão ou porcentagens**. Ex.: **30%** na versão A e **70%** na B; **cookie de experimento** para manter a mesma experiência; métricas de cada versão. Reverte rápido **sem alterar o código** |
| **Load Balancing** (Figura 6) | Algoritmos **round-robin, least request ou random**; políticas por **latência**; **priorizar instâncias** em manutenção ou testes. Pode usar critérios como **latência, uso de CPU** ou **least requests** (menor número de requisições ativas); balancear entre **zonas ou regiões**; integrar-se à **descoberta de serviço** para mandar tráfego só a instâncias **saudáveis** |
| **Traffic Mirroring** (Shadowing) | **Duplica** as requisições da versão estável para a nova, **só para monitoramento** (a resposta não é usada); avalia desempenho, métricas e logs com **tráfego real** antes do rollout, sem impactar os usuários |
| **Roteamento baseado em conteúdo** | Por atributos da requisição: **URL, cabeçalhos ou método HTTP** |
| **Fault Injection** | Simula **atrasos e erros HTTP** para testar a resiliência, prática essencial no [[Chaos Engineering]] |
| **Timeouts e retries** | Padrões de resiliência que **também** atuam como controle de tráfego |

- Em resumo, a rede vira uma **ferramenta programável e inteligente**.

## Padrões de resiliência no Service Mesh
- Falhas são **inevitáveis** em sistemas distribuídos; o Service Mesh aplica os padrões **na camada de rede**, de forma **transparente**.

| Padrão | O que o PDF diz |
|---|---|
| **Circuit Breaker** (Figura 7, Istio/Envoy) | **Fechado**: requisições normais; se as falhas (erros ou timeouts) excederem um limite num período → **aberto**. **Aberto**: rejeita **imediatamente**, sem tentar; após um **período de descanso**, vai a **meio-aberto**. **Meio-aberto**: uma **quantidade limitada** de requisições de teste; sucesso → **fechado**; senão → **aberto**, reiniciando o descanso. Benefícios: evita cascata, **falha rápido** e dá uma janela para o serviço se estabilizar. Ver [[Circuit Breaker]] |
| **Retry** | Nem toda falha é permanente (pico de carga, rede, reinicialização). Sem entender o comportamento da aplicação, **pode** agravar o problema; boas práticas: **número máximo de retentativas, backoff exponencial, jitter e idempotência**. Ver [[Retry e Backoff Exponencial]] |
| **Timeout** | Tempo máximo que o chamador aguarda; excedido, a requisição é **cancelada** e uma **falha controlada** é retornada. Sem timeout: bloqueio indefinido, esgotamento de **threads, conexões e memória**, reação em cadeia. Benefícios: **evita bloqueio de recursos**, **melhora a responsividade** (falhar rápido) e **ajuda a identificar gargalos**. Ver [[Timeout]] |

- **Circuit Breaker e Retry**: na aula anterior, foram implementados **no código**. Com **Istio ou Linkerd**, são configurados **no Control Plane** (o Circuit Breaker de forma **declarativa**; no retry, número de retentativas, tempo limite, backoff e jitter) e os sidecars os aplicam **sem alterar nenhuma linha de código**, com **consistência** em toda a malha.
- **Timeout**: implementá-lo à mão exige manutenção contínua e repetição de lógica em várias linguagens e frameworks; com **Istio ou Linkerd**, a configuração se torna **centralizada e transparente**.

## Evolução e posição na arquitetura
- Monólitos (chamadas de função, bibliotecas) → **SOA** nos anos 2000 (**SOAP** e **REST**) → microsserviços, com centenas de serviços duplicando retry, Circuit Breaker, balanceamento e observabilidade.
- O Service Mesh é uma evolução em relação a **proxies reversos** e **API Gateways**: o **API Gateway** atua **na borda** (tráfego externo); o Service Mesh **permeia toda a malha** (comunicação interna). Ver [[API Gateway]].

## Implementações
| | **Istio** | **Linkerd** | **Consul Connect** |
|---|---|---|---|
| Origem | **Google, IBM e Lyft**; o mais conhecido e adotado | **Buoyant** | Ecossistema **HashiCorp** |
| Arquitetura | **Envoy** no Data Plane; Control Plane com **Pilot** (descoberta e tráfego), **Citadel** (certificados e segurança), **Galley** (validação e distribuição de configurações) e **Mixer** (telemetria e políticas, **descontinuado**) | Control Plane **enxuto** e proxies em **Rust** muito leves | Integração **nativa com o Consul** para descoberta; Data Plane flexível (diferentes proxies ou **SDKs** na aplicação) |
| Força | **Flexibilidade** e amplo conjunto de funcionalidades (ex.: **mTLS** automático e políticas por atributos como **JWT**) | **Simplicidade e performance**: **menor consumo de recursos**, latência quase imperceptível; adoção rápida | Útil para quem já usa HashiCorp, ambientes **híbridos e multi-cloud** e integração com infraestrutura existente |
| Custo | Curva de aprendizado **íngreme** | Menos roteamento avançado e políticas granulares | — |

- **Não há solução única**: a escolha depende de flexibilidade, simplicidade, performance e integração com o ecossistema da organização.
- O mesh fornece métricas como **latência P99**, **uso de CPU dos proxies** e **taxa de connection pool**.

## Tendências
| Tendência | O que o PDF diz |
|---|---|
| **Ambient Mesh** | Introduzido pelo **Istio**; elimina a necessidade de **sidecars** para todos os serviços |
| **eBPF** | Código seguro **no kernel Linux**, performance quase nativa; meshes baseados em eBPF, como o **Cilium**, reduzem o overhead |
| **WebAssembly (WASM)** | **Plugins** em Rust, Go ou C++ executados **dentro dos proxies** (ex.: autorização personalizada, manipulação de headers) |

- Por que é fundamental: externaliza a lógica de resiliência para a **infraestrutura**, com políticas **uniformes**; é "a sua **apólice de seguro** contra o caos dos microsserviços".

## Referências
Calcote e Butcher, *Istio: up and running* · FluxCD: Flagger, Gateway API Canary Deployments, Istio A/B testing · Google Cloud: Service Mesh load balancing · Istio: Circuit breaking · Medium/Google Cloud: managed vs unmanaged Service Mesh · Redthunder: Circuit breaker in service mesh · Target: Service Mesh
