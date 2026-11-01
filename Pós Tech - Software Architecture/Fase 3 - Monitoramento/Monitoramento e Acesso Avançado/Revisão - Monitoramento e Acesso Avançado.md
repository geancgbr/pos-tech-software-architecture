---
tags: [pos-tech/fase-3, monitoramento, revisao]
disciplina: Monitoramento e Acesso Avançado
---

# Revisão - Monitoramento e Acesso Avançado

[[Monitoramento e Acesso Avançado]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - APM e SRE
> [!question]- O que são SLI, SLO e SLA?
> SLI: métricas quantitativas de qualidade (latência, erros, disponibilidade). SLO: metas mensuráveis baseadas nos SLIs, menos formais e sem penalidades. SLA: contratos formais, geralmente com penalidades. → [[SLI, SLO e SLA]]

> [!question]- Qual a relação entre SLI, SLO e SLA?
> SLI → SLO → SLA: medimos com SLIs, definimos metas internas com SLOs e fazemos promessas externas com SLAs.

> [!question]- O que é o Error Budget, e como é calculado?
> A quantidade aceitável de tempo de indisponibilidade num período, calculada com base no SLA ou no SLO. Equilibra lançar recursos com manter a estabilidade. → [[Error Budget]]

> [!question]- O que acontece quando o Error Budget é consumido?
> As equipes podem ser incentivadas a focar em estabilidade em vez de lançar recursos, até o serviço voltar aos níveis acordados.

## Aula 2 - APM com Datadog
> [!question]- O que é um sidecar, e por que usá-lo?
> Instrumentar a partir de outro servidor/container: é transparente, não usa os recursos da aplicação e garante o envio de erros mesmo se o container morrer. Aumenta um pouco os custos (um host exclusivo por aplicação). → [[Sidecar]]

> [!question]- Que métricas de rastreamento o Datadog coleta?
> Contagem de requisições, contagem de erros e latência, calculadas sobre 100% do tráfego.

> [!question]- Segundo o PDF, o que indicam os levels 500 e 400?
> O 500 pode indicar que a request nem chegou ao destino; o 400 indica que chegou, mas houve um erro (como não autorizado).

## Aula 3 - Logs com Datadog
> [!question]- Quais as categorias de severidade de logs?
> Debug, Info, Notice, Warning, Error, Critical, Alert e Emergency. → [[Severidade e Tipos de Logs]]

> [!question]- Quais os 7 tipos principais de logs?
> Sistema, aplicação, segurança, transação, auditoria, eventos e erros.

> [!question]- Onde se encontram logs de segurança no Windows, Linux e macOS?
> Security Event Log, `/var/log/auth.log` e Console de Segurança.

## Aula 4 - Infra com Datadog
> [!question]- O que significam as cores do Host Map?
> Cinza: perda de comunicação. Vermelho: problema de CPU. Laranja: problema de desempenho. Verde: comunicação e desempenho ok. → [[MAV 04 - Infra com Datadog]]

> [!question]- Como o Host Map ajuda a economizar na AWS?
> Agrupando por instance type e por função, acham-se hosts subutilizados que podem ir para instâncias mais baratas (no exemplo, 7 nós c3.2xlarge → c3.xlarge, cerca de US$ 12.877,20/ano).

> [!question]- Para que serve o catálogo de recursos da integração com a cloud?
> Analisar os recursos da nuvem sem precisar de acesso à cloud, com cobertura de segurança, visão do cenário e inventário. A integração é cobrada por ingest.

## Aula 5 - Alertas com Datadog
> [!question]- Quais benefícios o alerta proativo traz?
> Menor MTTD e MTTR, melhor experiência do usuário, eficiência operacional e prevenção de perdas financeiras. → [[Monitors do Datadog]]

> [!question]- Quais os métodos de detecção de um monitor?
> Threshold (limiar estático), Anomaly (ML aprende o normal), Forecast (ML prevê que um limiar será cruzado) e Outlier (um membro do grupo se comporta diferente).

> [!question]- Quais os tipos de monitores?
> Metric, APM (Trace & Span Analytics, Error Tracking, SLOs), Log, Synthetic (API e Browser Tests) e Composite (AND, OR, NOT).

> [!question]- O que é a fadiga de alerta, e como evitá-la?
> Excesso de falsos positivos ou alertas de baixa prioridade faz as pessoas ignorarem os alertas. Ajustar thresholds, usar janelas apropriadas, não alertar sobre tudo e priorizar.

## Aula 6 - Dashboards com Datadog
> [!question]- Timeboard × Screenboard?
> Timeboard: análise temporal, eixo de tempo global e sincronizado, layout estruturado. Screenboard: layout livre, cada widget pode ter seu próprio intervalo, mais widgets não temporais. → [[Dashboards do Datadog]]

> [!question]- Para que servem as variáveis de template?
> Para dashboards dinâmicos e reutilizáveis: um dropdown (ex.: `$env`, `$service`) filtra todos os widgets que usam a variável.

## Aula 7 - New Relic e Apdex
> [!question]- O que é o Apdex, e como se calcula?
> Padrão da indústria para a satisfação com o tempo de resposta: (satisfeitas + tolerantes/2) / total, de 0 a 1. → [[Apdex]]

> [!question]- Como se classificam as solicitações no Apdex?
> Satisfeitas: ≤ T. Tolerantes: > T e ≤ 4T. Frustradas: > 4T ou erro no servidor.

> [!question]- Qual é a faixa ideal de Apdex?
> 0,85 a 0,95 (azul).

## Aula 8 - Logs com New Relic
> [!question]- O que são os Logs in Context?
> Logs exibidos no contexto de outras telas (APM, infraestrutura, distributed tracing, Errors Inbox), para chegar mais rápido à causa raiz. → [[Logs in Context]]

> [!question]- Por que não usar log decoration com o encaminhamento do agente ao mesmo tempo?
> O log seria enviado duas vezes, o que pode gerar cobrança dupla.

## Aula 9 - Infra com New Relic
> [!question]- Cite boas práticas de infraestrutura no New Relic.
> Agente em todo o ambiente, integração com o EC2, ativar integrações, visualizações de grupos de hosts, alertas por tags, infraestrutura junto do APM e dados via NRQL. → [[MAV 09 - Infra com New Relic]]

> [!question]- O que é NRQL?
> A linguagem de consulta do New Relic, semelhante ao ANSI SQL. → [[NRQL]]

## Aula 10 - Configurando alertas
> [!question]- Como funcionam os alertas no New Relic?
> Segundo os conceitos da aula (Figura 1, fonte New Relic), uma política inclui condições com limites; violado um limite, um incidente é acionado; com um workflow, você é notificado.

> [!question]- Por que nomes de alerta claros?
> Para que o nome diga conta, região, serviço e causa aparente (ex.: `AWS-Instancia01-Prod-SP-CPU-Critical`).

> [!question]- O que é um runbook?
> Um conjunto de procedimentos para manter uma rotina de trabalho padronizada: quem, ferramentas, recursos, prazo e problemas comuns. → [[Runbook]]

> [!question]- Por que automatizar alertas com Terraform?
> Evita alterações não documentadas, dá rastreabilidade e padronização e documenta os alertas.

## Aula 11 - Dashboards com New Relic
> [!question]- Qual a estrutura de uma query NRQL?
> SELECT ... FROM DataType [WHERE] [FACET] [LIMIT] [SINCE] [UNTIL] [COMPARE WITH] [TIMESERIES]. FACET é como o GROUP BY. → [[NRQL]]

> [!question]- Data Explorer × Query Builder?
> Data Explorer: descobrir os tipos de dados e atributos. Query Builder: escrever e testar queries.

> [!question]- Cite widgets de dashboard do New Relic.
> Line/Area/Bar, Billboards, Tables, Pie/Donut, Histograms, Funnels, Gauges e Text/Markdown.

## Aula 12 - Contexto Map
> [!question]- Para que servem os Service Maps?
> Entender a arquitetura, detectar problemas e sua propagação, analisar o Blast Radius, achar gargalos e otimizar. São construídos com os dados do APM, especialmente do tracing distribuído. → [[MAV 12 - Contexto Map New Relic]]

> [!question]- Quais os elementos de um mapa de serviço?
> Nós (serviços APM, datastores, serviços externos, apps Mobile/Browser), arestas (chamadas), indicadores de saúde por cor e métricas nas conexões (throughput, latência média, taxa de erro).

> [!question]- O que é um Workload?
> Um agrupamento lógico de entidades que representa uma funcionalidade de negócio (ex.: Processamento de Pagamentos), com visão de saúde e mapa de dependências.

## Dúvidas em aberto
- Aula 1: o resumo cita Golden Metrics, Tracing, OpenTelemetry e o papel do SRE, mas o texto só desenvolve SLI, SLO, SLA e Error Budget.
- Aula 2: a frase sobre usar o sidecar "somente para ambientes produtivos, ambientes de Staging e Development" é ambígua.
- Aula 7: o exemplo usa T = 0,5 s, mas a explicação dos tolerantes usa "4 x 1,2 = 4,8 segundos"; e as duas últimas faixas de cor aparecem como "0.85-0.95" e "0.95".
- Aulas 7 a 10: os cabeçalhos internos dizem "AULA 05" a "AULA 08".

## Pontos fracos (o que errei)
