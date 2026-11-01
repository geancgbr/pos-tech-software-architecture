---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, aula]
disciplina: OpenTelemetry
aula: 5
fonte: "OpenTelemetry/Aula 05 - Boas práticas e desafios .pdf"
---

# OTEL 05 - Boas práticas e desafios

← [[OTEL 04 - OpenTelemetry Logs (Loki)]] · [[OpenTelemetry]]

> [!summary] Em uma frase
> O valor da observabilidade está na **correlação entre os pilares**, com o **TraceId** como fio condutor. Boas práticas: **[[Convenções Semânticas|convenções semânticas]]**, instrumentação **automática + manual**, o **Collector** como intermediário e **controle da [[Cardinalidade|cardinalidade]]**. Desafios: **overhead, custo, curva de aprendizagem e código legado**. Futuro: **[[Tendências da Observabilidade (eBPF, Profiling e AIOps)|eBPF, continuous profiling, AIOps]]** e uma **cultura** de observabilidade.

## Hands On
Revisar o código construído e discutir onde a **instrumentação manual** agregaria **valor de negócio**. Planejar uma **arquitetura de coletores** para produção e debater decisões sobre **amostragem** e **controle de cardinalidade**.

## A narrativa da depuração moderna
A observabilidade não é ter **três ferramentas separadas**, e sim uma **compreensão unificada** do sistema.

| Etapa | Sinal | Exemplo do PDF | Pergunta respondida |
|---|---|---|---|
| 1. **O alerta** | **Métrica** | No Grafana (com Prometheus), a latência **p99** do `checkout-service` disparou | **O que** está errado? A latência está alta |
| 2. **O contexto amplo** | **Trace** | No Jaeger ou no **Grafana Tempo**, um trace exemplar lento; a visualização em **cascata (Gantt chart)** mostra o `inventory-service` demorando segundos | **Onde** está o gargalo? Na comunicação com o serviço de inventário |
| 3. **A causa raiz** | **Log** | Pelo TraceId, os logs do serviço naquele momento: "ERROR: Could not acquire database connection from pool. Timeout expired." | **Por que** está lento? O **pool de conexões** do banco está esgotado |

Do **"que"** ao **"onde"** e ao **"por que"**, uma jornada que **pode ser feita em minutos em vez de horas**. O OpenTelemetry garante que o **TraceId** seja **o fio condutor** que costura todos os sinais.

## Boas práticas fundamentais
**1. Abrace as convenções semânticas**
- **Por quê**: se o serviço de pagamentos chama o status HTTP de `http.status_code` e o de frete de `response_code`, perdem-se as **consultas unificadas** e os **dashboards consistentes**.
- **Ação**: familiarizar a equipe com as convenções dos recursos usados (HTTP, banco, mensageria), na instrumentação automática **e** na manual. Isso cria uma **linguagem comum** de telemetria.

**2. Combine instrumentação automática e manual**
- **Automática como base**: sempre comece por ela. **Cobertura ampla com esforço mínimo**: o "big picture" instantâneo.
- **Manual para o contexto de negócio**: spans para fluxos importantes (`process-refund`, `generate-invoice`), com atributos de negócio (`customer.tier`, `product.category`, `is_trial_user`). Responde perguntas como "A nova funcionalidade de recomendação está impactando a latência para usuários premium?".

**3. O OpenTelemetry Collector é seu melhor amigo**
Resista a exportar direto da aplicação para o back-end final; use o Collector como intermediário. Ver [[OpenTelemetry Collector]].
- **Desacoplamento** (a principal vantagem): as aplicações só falam **OTLP**. Migrar do Jaeger para um fornecedor comercial, ou adicionar outro back-end, muda **só a configuração do Coletor**, sem alterar código nem fazer deploy.
- **Processamento centralizado**:
  - **Amostragem tail-based**: políticas inteligentes para capturar **100% dos erros** sem sobrecarregar o back-end de traces.
  - **Filtragem de dados sensíveis (PII)**: remover informações pessoais, senhas ou chaves de API **antes que saiam da infraestrutura**, em conformidade com a **LGPD/GDPR**.
  - **Enriquecimento de metadados**: região da nuvem, ID do cluster Kubernetes, versão da aplicação.
  - **Eficiência de rede**: agregar, comprimir e enviar em **lotes (batches)**.

**4. Gerencie a cardinalidade de forma proativa**
- **Cardinalidade**: o **número de valores únicos** de um atributo (ou label, no Prometheus e no Loki). Alta cardinalidade é **um dos maiores desafios técnicos e de custo**.
- **O problema**: cada combinação única de labels cria uma **nova série temporal** no Prometheus e um **novo fluxo** no Loki. Atributos de cardinalidade infinita (`user_id`, `request_id`, `trace_id`) como labels causam uma **"explosão de cardinalidade"**, que pode **derrubar o back-end**.

| Back-end | O que fazer |
|---|---|
| **Métricas (Prometheus)** | **Nunca** usar atributos de alta cardinalidade como labels. Usar dimensões de baixa a média cardinalidade (`http_method`, `status_code_class` (2xx, 4xx, 5xx), `service_version`) |
| **Logs (Loki)** | Labels para **metadados de infraestrutura** (cluster, namespace, pod, service) e **severidade**. Identificadores de alta cardinalidade (`user_id`, `trace_id`) ficam **no corpo** do log |
| **Traces (Jaeger)** | São **projetados para alta cardinalidade**: dá para pôr `user_id` nos spans. A indexação é otimizada para isso |

## Desafios comuns e mitigação
| Desafio | Mitigação |
|---|---|
| **Overhead de performance** ([[Amostragem (Sampling)\|amostragem]]): coletar telemetria consome CPU e memória. Instrumentação muito agressiva, sobretudo em aplicações de alta performance e baixa latência, pode gerar overhead perceptível | **Amostragem**, a principal ferramenta contra o overhead de tracing: **head-based** (por proporção) no SDK, combinada com **tail-based** no Coletor para reter os traces importantes · **ajuste do SDK** (tamanho dos lotes, intervalos de exportação, limites de fila) · **Coletor como agente em cada nó** (**DaemonSet** no Kubernetes) em vez de um deployment centralizado, para distribuir a carga e minimizar saltos de rede |
| **Volume de dados e custo**: dados têm custo de armazenamento, transferência e processamento, e **os custos** podem sair do controle rapidamente | **Amostragem agressiva** dos traces bem-sucedidos (muitas vezes **1% a 5%** basta), mantendo **100% dos traces com erro** · **políticas de retenção** diferentes (ex.: traces por dias, métricas por meses, logs agregados por um ano) · **filtragem no Coletor** (ex.: descartar logs de **DEBUG** em produção ou métricas de **health checks**) |
| **Curva de aprendizagem**: OTel, Prometheus, Loki, Jaeger, PromQL... | **Comece simples** (um serviço, um objetivo claro, instrumentação automática) · **treinamento** (workshops, documentação, **"campeões/campeãs" de observabilidade**) · **dashboards padronizados** no Grafana |
| **Código legado e de terceiros** ("caixa preta") | **Exporters e agentes** (provavelmente já existe um exporter do Prometheus ou integração do OTel) · **Proxy/Service Mesh** (Istio, Linkerd, NGINX, Envoy geram spans e métricas do tráfego, sem tocar no código) · **Logs como fonte** (se tudo mais falhar, os logs podem ser a única fonte: o Collector analisa logs de acesso e pode **gerar métricas** a partir deles, como contar logs de erro) |

## O futuro da observabilidade
**eBPF: observabilidade sem instrumentação**
- **O que é**: o **Extended Berkeley Packet Filter**, tecnologia **dentro do kernel do Linux** que executa programas num **sandbox** no kernel, **sem alterar o código do kernel nem carregar módulos**.
- **Impacto**: agentes eBPF **podem observar** **chamadas de sistema, tráfego de rede e interações entre processos**, coletando métricas, traces e logs "de ouro" (como dados **RED**: Rate, Errors, Duration) **sem instrumentar o código**.
- **OTel e eBPF**: projetos como **Cilium** e **Pixie** (da New Relic) coletam com eBPF e exportam em **OTLP**. O futuro provável é uma **combinação**: eBPF para a visibilidade universal de infraestrutura e rede, e a instrumentação do OTel para o **contexto de negócio**.

**O quarto pilar: continuous profiling**
- Analisa **constantemente** o consumo de **CPU** e a **alocação de memória** em produção, **até o número da linha** no código.
- **Complementa**: o trace diz que um span é lento; o **profiler** diz **qual função e qual linha** dentro dele consome 80% da CPU.
- Visualizado em **"flame graphs"**. Exemplo de back-end: o **Pyroscope**, recentemente fundido com o **Grafana Phlare**. O OTel já trabalha para **padronizar um modelo de dados para profiles**.

**AIOps (Inteligência Artificial para Operações)**
- Aplicação de **Machine Learning e IA** aos dados de observabilidade, porque a análise manual se torna impraticável.
- **Aplicações**: **detecção de anomalias** (desvios que alertas por limiar não pegariam) · **correlação de eventos** (identificar a causa raiz provável automaticamente) · **análise preditiva** (prever falhas por tendências históricas).
- O OTel, com dados **estruturados e padronizados**, é a **fonte ideal** para esses modelos.

## A cultura de observabilidade
A observabilidade é **mais que um conjunto de ferramentas: é uma mudança cultural**.

| Cultura de monitoramento tradicional | Cultura de observabilidade |
|---|---|
| Uma **equipe central de Ops** mantém as ferramentas; os devs são **consumidores passivos** | **Responsabilidade compartilhada** |

- **"You Build It, You Run It, You Own It"**: as equipes de desenvolvimento são **donas dos serviços em produção**, inclusive da observabilidade.
- **Devs como instrumentadores**: sabem o que importa instrumentar e passam a ver a instrumentação como **parte do ciclo de desenvolvimento**, **como os testes unitários**.
- **Dados para todos**: gerentes de produto (uso de funcionalidades), negócios (**SLOs**) e devs (impacto do código antes da produção).

O objetivo final é uma cultura em que as equipes se sentem **capacitadas a fazer perguntas** sobre seus sistemas e têm as ferramentas para respondê-las.

## Referências
Grafana: Pyroscope and Grafana Phlare Join together... · OpenTelemetry: Collector Deployment Patterns · OpenTelemetry: Sampling
