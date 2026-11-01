---
tags: [pos-tech/fase-3, monitoramento, sre, conceito]
aliases: [SLI, SLO, SLA, SLOs, SLIs, Service Level Objective, Service Level Agreement, Service Level Indicator]
---

# SLI, SLO e SLA

Os principais termos do **SRE**, junto com o [[Error Budget]].

| | SLI | SLO | SLA |
|---|---|---|---|
| Nome | Indicador de Nível de Serviço | Objetivo de Nível de Serviço | Acordo de Nível de Serviço |
| O que é | **Métricas quantitativas** de aspectos-chave da qualidade (latência, taxa de erros, disponibilidade) | **Metas específicas e mensuráveis**, geralmente **baseadas nos SLIs** | **Contratos formais** entre provedor e usuários |
| Formalidade | — | **Menos formal**, **sem penalidades** | Geralmente **com penalidades** |
| Uso | Medir desempenho e saúde de forma objetiva | Orientar desenvolvimento e operações | Expectativas claras e **responsabilização** |

- **SLI → SLO → SLA**: medimos com SLIs, definimos **metas internas** com SLOs e fazemos **promessas externas** com SLAs ([[MAV 01 - O que é APM e seus benefícios]]).
- **Aula 10**: os SLIs permitem monitorar continuamente e achar problemas **antes que afetem os usuários**; os SLOs são **metas quantitativas** (disponibilidade, tempo de resposta), baseadas nas necessidades dos clientes, e dão uma compreensão compartilhada das expectativas. São uma boa prática para **alertas** ([[MAV 10 - Configurando alertas]]).
- **No Datadog**: monitores de **SLO** (ex.: 99,9% de requests com sucesso) alertam sobre o error budget consumido ([[MAV 05 - Criando alertas com DD]]). Dashboards acompanham SLOs e KPIs ([[MAV 06 - Criando dashboards com DD]]).
- **Apdex**: segundo a New Relic, "uma solução simplificada de SLA" ([[Apdex]]).

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
- **SLO** de exemplo: nos últimos 7 dias, 95% das requisições com resposta < 2 s. **SLA** de exemplo: 90% das operações do mês em até 2 s, "normalmente baseado nos SLOs".
- **Como usar**: identificar SLIs → definir SLOs realistas e desafiadores → monitorar os SLIs e configurar alertas baseados nos SLOs → se aplicável, formalizar num SLA. **Boas práticas**: revisão periódica, equilíbrio e transparência ([[MS2 06 - Realizando o deploy de microsserviços, parte 2]]).

## Na disciplina Resiliência em Microsserviços (Fase 4)
Os **SLOs** estão entre as métricas de sucesso do [[Chaos Engineering]] ([[RES 05 - Chaos Engineering]]).

Aparece em: [[MAV 01 - O que é APM e seus benefícios]], [[MAV 05 - Criando alertas com DD]], [[MAV 10 - Configurando alertas]], [[MS2 06 - Realizando o deploy de microsserviços, parte 2]], [[RES 05 - Chaos Engineering]]
