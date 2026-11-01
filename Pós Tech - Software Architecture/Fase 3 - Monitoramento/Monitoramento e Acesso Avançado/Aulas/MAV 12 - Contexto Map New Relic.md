---
tags: [pos-tech/fase-3, monitoramento, newrelic, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 12
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 12_rev2.pdf"
---

# MAV 12 - Contexto Map New Relic

← [[MAV 11 - Criando dashboards com New Relic]] · [[Monitoramento e Acesso Avançado]]

> [!summary] Em uma frase
> Em arquiteturas distribuídas, um request atravessa dezenas de serviços. O **[[New Relic]]** oferece um **"contexto de mapa"** (**Service Maps**, Dependency Maps, Topology Views), construído com os dados da instrumentação (**APM**), especialmente do **tracing distribuído**: **nós** (entidades), **arestas** (chamadas), cores de saúde e métricas nas conexões. **Workloads** e **Lookout/Navigator** estendem essa visão.

## Hands On
Descobrir e interpretar os **Service Maps** (nós = serviços e bancos; conexões = chamadas), aplicar **filtros**, analisar a saúde dos componentes e navegar do mapa para **traces distribuídos, dashboards de APM e logs**.

## Por que mapas
De monólitos a **microsserviços**, a rede de interações cresce **exponencialmente**. Perguntas como "Qual serviço está causando lentidão?" ou "Se o serviço X falhar, quais outros serão impactados?" ficam difíceis sem as ferramentas certas.

| Para quê | O que o PDF diz |
|---|---|
| **Compreensão da arquitetura** | Ver como os componentes estão conectados **em tempo real** |
| **Detecção de problemas** | Quais serviços estão com problema e como esses problemas **podem estar se propagando** |
| **Análise de impacto (Blast Radius)** | O **alcance potencial** de uma falha num componente |
| **Identificação de gargalos** | Os pontos de lentidão no fluxo por vários serviços |
| **Otimização de performance** | **Caminhos críticos** e interações entre serviços |

- Os mapas são construídos **dinamicamente** a partir dos dados do **APM**, especialmente do **tracing distribuído**: agregando milhares de traces, o New Relic **infere** as relações entre os serviços.

## Os mapas no APM
- **Ponto de partida**: o **sumário do APM** de um serviço, ou abas como "Distributed tracing" e "Dependencies". Ali aparecem os serviços **dos quais o seu depende (upstream)** e os que **dependem dele (downstream)**.

| Elemento | O que é |
|---|---|
| **Nós (Nodes)** | As entidades: **serviços APM** (os seus), **datastores** (SQL, NoSQL, caches), **serviços externos** (APIs de terceiros não instrumentadas na sua conta) e **aplicações Mobile/Browser**, se relevantes no fluxo |
| **Arestas (Edges)** | As interações; a **seta** geralmente indica **quem chama quem**. Podem ser HTTP/HTTPS, **gRPC**, queries a bancos ou mensagens em filas |
| **Indicadores de saúde** | Cores, geralmente **verde** (saudável), **amarelo** (aviso), **vermelho** (crítico), baseadas em **Apdex**, taxa de erro ou alertas ativos |
| **Métricas nas conexões** | **Throughput** (RPM), **Average Latency** e **Error Rate** entre os dois nós |

## Interagindo com o mapa
- **Seleção**: clicar num nó **geralmente** abre detalhes e links para o APM, traces e logs; clicar numa conexão **pode** mostrar as métricas daquela interação e os traces que passam por ali.
- **Filtros e camadas**: em mapas mais complexos, **podem existir** opções de filtro por ambiente ou tags e para ocultar tipos (ex.: os datastores).
- **Destaque de caminhos (path highlighting)**: ao analisar traces distribuídos, **frequentemente é possível** ver o caminho do trace destacado no mapa.
- **Navegação contextual**, se um serviço aparece **vermelho**: (1) clicar e ver as métricas; (2) ir ao **sumário do APM** (erros, transações lentas, **JVM**); (3) examinar os **traces distribuídos**; (4) verificar os **logs contextuais**.

## Workloads e Lookout/Navigator
- **Workload**: um **agrupamento lógico** de entidades (serviços, hosts, bancos, apps Browser) que juntas representam uma **funcionalidade de negócio**, uma aplicação ou a área de uma equipe, com visão de saúde e **mapa de dependências**. Ex.: um Workload "**Processamento de Pagamentos**" com os microsserviços, bancos e APIs externas desse processo.
- **Lookout/Navigator** ("os nomes e funcionalidades exatas podem evoluir", diz o PDF): visão **panorâmica e em tempo real** de todo o ecossistema.
  - **Visão de helicóptero**: visualização em **"colmeia" (honeycomb)** ou grafos, cada célula colorida pela saúde, para achar os **"hotspots"**.
  - **Exploração intuitiva**: clicar nas entidades com problema e ir aos dashboards, traces ou logs.

## Mapas e tracing distribuído
O tracing distribuído **alimenta** muitos desses mapas. Cada trace é um "mapa" de uma requisição (geralmente um **gráfico de Gantt** de spans e durações). Os mapas agregados são **uma compilação estatística** de milhares ou milhões de traces, revelando os padrões de comunicação e os gargalos comuns.

## Casos de uso e considerações
- **Casos de uso**: diagnóstico de incidentes · otimização de performance · **planejamento de mudanças** (migração, refatoração, desativação) · **Blast Radius** · **onboarding** de novos membros · comunicação com stakeholders.
- **Qualidade da instrumentação**: a precisão do mapa depende do APM e da **propagação do contexto de tracing**; falhas geram mapas **incompletos**.
- **Complexidade visual**: em sistemas grandes, usar filtros, Workloads e navegação hierárquica.
- **Interpretação humana**: o mapa mostra **correlações e fluxos**, mas a **causalidade** ainda exige análise humana.

## Referências
New Relic: Distributed tracing · Service map: visualize your entities · Workloads: group related entities
