---
tags: [pos-tech/fase-3, monitoramento, newrelic, dashboards, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 11
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 11_rev2.pdf"
---

# MAV 11 - Criando dashboards com New Relic

← [[MAV 10 - Configurando alertas]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 12 - Contexto Map New Relic]]

> [!summary] Em uma frase
> Os **dashboards do [[New Relic]]** consolidam dados de **APM, Browser (RUM), Mobile, Infraestrutura e Logs** numa só visualização, e praticamente **tudo é alimentado por uma query [[NRQL]]**. Os widgets vão de **linhas** e **billboards** a **funis** e **histogramas**; **páginas** organizam e **variáveis** tornam o dashboard reutilizável.

## Hands On
Navegar pela interface de dashboards, pelo **Data Explorer** e pelo **Query Builder**, entender os fundamentos da **NRQL** e criar um dashboard com **linecharts**, **billboards**, **tabelas** e **pie charts**, vendo também **funis** e **histogramas**.

## A filosofia
Todos os dados coletados devem ser **facilmente acessíveis e consultáveis**. A **NRQL** é a protagonista: praticamente tudo num dashboard customizado vem de uma query NRQL.

## NRQL
Linguagem de consulta **semelhante ao SQL**, feita para consultar a base de telemetria do New Relic (**NRDB**).

```
SELECT function(attribute) | attribute | * FROM DataType
  [WHERE condition] [FACET attribute | dimensions()] [LIMIT number]
  [SINCE time_ago | timestamp] [UNTIL time_ago | timestamp]
  [COMPARE WITH time_ago] [TIMESERIES [time_interval | AUTO | MAX]]
```

| Cláusula | O que faz |
|---|---|
| **SELECT** | O que ver: uma função de agregação (`average(duration)`, `count(*)`, `sum(totalValue)`, `uniques(userId)`), um atributo ou `*` |
| **FROM** | O tipo de dado: **Transaction** (backend/APM), **PageView** (frontend/Browser/RUM), **SystemSample** (infraestrutura), **Log**, **Metric** |
| **WHERE** | Filtra (ex.: `appName = 'MinhaLojaOnline'`, `httpResponseCode >= 500`, `countryCode = 'BR'`) |
| **FACET** | **Agrupa** por atributos, criando várias séries ou linhas (como o **GROUP BY** do SQL) |
| **LIMIT** | Restringe o número de **facetas** |
| **SINCE / UNTIL** | O período: relativo (`SINCE 1 hour ago`) ou absoluto |
| **COMPARE WITH** | Compara com um período anterior (`COMPARE WITH 1 day ago`) |
| **TIMESERIES** | Vira **série temporal** (ex.: `TIMESERIES 5 minutes` ou `AUTO`) |

- **Data Explorer**: descobrir quais **tipos de dados e atributos** existem na conta. **Query Builder**: escrever e testar queries, vendo o resultado em **JSON** ou num gráfico básico.

## Widgets
| Widget | Para quê | NRQL típica do PDF |
|---|---|---|
| **Line, Area, Bar Charts** | Tendências ao longo do tempo (latência, throughput, erro, CPU). `FACET` + `TIMESERIES` = várias linhas | `SELECT average(duration) FROM Transaction WHERE appName = 'MeuServicoAPI' TIMESERIES AUTO` |
| **Billboards** | **Um valor** em destaque (KPI), com **thresholds** que mudam a cor | `SELECT count(*) FROM PageView WHERE appName = 'MeuWebApp' SINCE 30 minutes ago` |
| **Tables** | Listas detalhadas, vários atributos; `FACET` define as linhas | `SELECT latest(hostName), average(cpuPercent), average(memoryUsedBytes) FROM SystemSample FACET entityName LIMIT 20` |
| **Pie / Donut Charts** | **Proporção** de categorias (navegador, dispositivo, país, status HTTP) | `SELECT count(*) FROM PageView WHERE appName = 'MeuWebApp' FACET deviceType` |
| **Histograms** | **Distribuição de frequência** em buckets; dispersão da latência e outliers | `SELECT histogram(duration, width: 100, buckets: 20) FROM Transaction WHERE appName = 'MeuServicoAPI'` |
| **Funnels** | **Progressão dos usuários** por etapas; gargalos de conversão | `SELECT funnel(userSessionId, WHERE pageUrl LIKE '%/carrinho' AS 'Carrinho', ...) FROM PageView` |
| **Gauges** | Um valor em relação a mínimo e máximo, ou % de um objetivo (Apdex, sucesso) | `SELECT percentage(count(*), WHERE error IS false) FROM Transaction WHERE appName = 'MeuServicoAPI'` |
| **Text/Markdown** | Títulos, descrições, links: contexto | — |

## Organização e interatividade
- **Páginas**: como **abas**, para dashboards complexos.
- **Variáveis de template**: "assim como no Datadog". Preenchidas por uma **query NRQL** (ex.: lista de appNames) ou com valores fixos; referenciadas como **`{{nomeDaVariavel}}`** (ex.: `WHERE appName = '{{selectedApp}}'`). Um dashboard serve a várias aplicações ou regiões.
- **Permissões e compartilhamento** (permalinks; alguns dashboards podem ser públicos, com cuidado) · **Modo Kiosk** (monitores de NOC, com rotação automática) · **Exportar/Importar JSON**.

## Melhores práticas
**Domine a NRQL** (use o Query Builder) · **conheça seus dados** (Data Explorer) · **otimize as queries** (evite `FACET` com **alta cardinalidade sem LIMIT**) · **foco e clareza** (use páginas) · **visualização apropriada** · **consistência** · **use variáveis** · **itere e refine**.

> [!note] O sumário do PDF mostra uma seção "Mercado, cases e tendências" com "Erro! Indicador não definido." (erro de formatação do documento).

## Referências
New Relic: Create custom data visualizations with dashboards · NRQL reference · Template variables
