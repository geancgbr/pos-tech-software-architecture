---
tags: [pos-tech/fase-3, monitoramento, datadog, dashboards, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 6
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 6_rev2.pdf"
---

# MAV 06 - Criando dashboards com DD

← [[MAV 05 - Criando alertas com DD]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 07 - Introdução APM New Relic]]

> [!summary] Em uma frase
> Os **dashboards** do **[[Datadog]]** transformam métricas, traces e logs em **visualizações claras e acionáveis**. Há dois tipos: **Timeboards** (eixo de tempo **global e sincronizado**) e **Screenboards** (layout **livre**). São montados com **widgets** e ficam dinâmicos com **variáveis de template**. Ver [[Dashboards do Datadog]].

## Hands On
Construir um **Timeboard** do zero (widgets **Timeseries**, **Query Value** e **Top List**) e um **Screenboard** (arrastar e soltar, com **Free Text**, **Image** e **Geomap**), usar **variáveis de template** e configurar **compartilhamento e permissões**.

## Para que serve um dashboard
**Monitoramento em tempo real** · **análise de tendências** · **diagnóstico e troubleshooting** (correlacionar métricas e logs num lugar só) · **comunicação e colaboração** entre equipes e stakeholders · **acompanhamento de metas** (SLOs e KPIs).

## Timeboards × Screenboards
| | Timeboards | Screenboards |
|---|---|---|
| Foco | **Análise temporal** | **Flexibilidade** de layout e conteúdo |
| Tempo | Todos os widgets **compartilham um eixo de tempo global e sincronizado** | Pode haver seletor global, mas **cada widget pode ter seu próprio intervalo** |
| Layout | Mais **estruturado**, em linhas e colunas | **Totalmente livre**, como uma "tela de pintura digital" (arrastar, soltar, redimensionar, até sobrepor) |
| Recursos | Zoom em gráficos, seleção de áreas, **sobreposição de eventos** (deploys, alertas, mudanças de configuração) | Mais **widgets não temporais** (texto, imagens, **iframes**, widgets de status) |
| Casos de uso | **Investigação de incidentes**, **análise pós-deploy**, **exploração de dados** | Dashboards de status (**NOC Displays**), relatórios para liderança, visualizações de arquitetura, dashboards de equipe |

## Widgets essenciais
| Widget | O que mostra | Exemplo do PDF |
|---|---|---|
| **Timeseries** | Métricas **ao longo do tempo** (linhas, barras, áreas; várias métricas no mesmo gráfico, cores, eixos Y duplos; overlay de eventos e anomalias do **Watchdog**). Query como `avg:system.cpu.user{env:production} by {host}` | CPU média, p95 e taxa de erros de um serviço nos últimos 60 min |
| **Query Value** | O **valor numérico único e mais recente** de uma consulta, com formatação condicional | Usuários ativos agora; taxa de erro atual do login |
| **Top List** | **Ranking** dos principais itens de uma métrica | 5 endpoints com maior p99; 3 serviços com maior erro |
| **Table** | Dados em **tabela**, cada coluna com uma query | Por microsserviço: requests, erro, p50, p90, p99 |
| **Note/Free Text** | Texto em **Markdown**, títulos e links (mais em Screenboards) | — |
| **Image** | Imagens estáticas ou dinâmicas (mais em Screenboards) | Logos, diagramas de arquitetura |
| **Geomap** | Métricas por **localização** (requer tags como `country_code`) | Requests por país; latência por região |

## Variáveis de template
- Definidas **no nível do dashboard** (ex.: `$service`, `$env`, `$host`), normalmente populadas com os valores de uma **tag**.
- Usadas nas queries no lugar de valores fixos: `avg:system.cpu.user{env:$env, service:$service}`.
- O dashboard mostra um **dropdown**, e todos os widgets que usam a variável se atualizam.
- **Benefícios**: **reutilização** (um dashboard para vários serviços, ambientes ou hosts), **consistência** e **exploração facilitada**.

## Compartilhamento e outras funcionalidades
- **Compartilhamento** com usuários ou equipes; **Screenboards** podem ter **URLs públicas** (com token ou abertas), com cautela conforme a sensibilidade dos dados.
- **Permissões**: quem vê e quem edita.
- **Modo TV / Dark Mode**: para monitores de **NOC**, com atualização automática.
- **Exportar/Importar JSON**: backup, **versionamento** (num Git) ou replicar em outra conta.
- **Favoritos** e nomes e descrições claros.

## Melhores práticas
**Defina o propósito e a audiência** (SRE investigando ≠ gerente de produto acompanhando KPIs) · **comece simples e itere** ("melhor vários dashboards focados do que um único poluído") · **conte uma história** (da visão geral ao detalhe) · **clareza visual** (títulos claros, cores consistentes, sem sobrecarga, espaço em branco) · **considere a performance** (muitos widgets ou queries complexas demoram) · **variáveis de template com sabedoria** · **documente** com um widget Note · **revise e obtenha feedback**.

> [!note] As referências do PDF desta aula são as mesmas da aula 5 (Monitors e Variables).

## Referências
Datadog: Getting started with Monitors · Monitor Types · Variables
