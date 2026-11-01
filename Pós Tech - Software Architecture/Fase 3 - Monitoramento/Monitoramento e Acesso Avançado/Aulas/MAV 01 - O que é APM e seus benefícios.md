---
tags: [pos-tech/fase-3, monitoramento, sre, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 1
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 1_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 01 - O que é APM e seus benefícios

[[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 02 - Introdução APM Datadog]]

> [!summary] Em uma frase
> Os principais termos do **SRE** são **SLI, SLO, SLA e Error Budget**. Medimos o serviço com **SLIs**, definimos metas internas com **SLOs** e fazemos promessas externas com **SLAs**. O **Error Budget** é a quantidade aceitável de indisponibilidade e equilibra **lançar recursos** com **manter a estabilidade**. Ver [[SLI, SLO e SLA]] e [[Error Budget]].

> [!note] O que está só no resumo
> Segundo o "O que vem por aí" e o "O que você viu", a aula também trata de **APM e seus benefícios**, das **Golden Metrics** (Response Time, Throughput, Errors e Latência), de **Tracing e OpenTelemetry**, da necessidade de **logs centralizados** para juntá-los com o Tracing e do **papel do SRE** na APM. O texto do PDF (Saiba Mais) só desenvolve SLI, SLO, SLA e Error Budget.

## Hands On
Aprofundar os conhecimentos sobre **APM, Golden Metrics, Tracing, Logging e SRE**.

## Os principais termos do SRE
| Termo | Definição | Uso |
|---|---|---|
| **SLI** (Indicadores de Nível de Serviço) | **Métricas quantitativas** de aspectos-chave da qualidade do serviço, como **latência, taxa de erros, disponibilidade** | **Medir o desempenho e a saúde** do serviço, de forma objetiva |
| **SLO** (Objetivos de Nível de Serviço) | **Metas específicas e mensuráveis** de desempenho, geralmente **baseadas nos SLIs**. **Menos formais** que os SLAs e **sem penalidades** | **Orientar o desenvolvimento e as operações**; mostrar o quão bem o serviço atende às expectativas dos usuários |
| **SLA** (Acordos de Nível de Serviço) | **Contratos formais** entre o provedor e seus usuários com os níveis esperados. Geralmente incluem **penalidades** se não forem atendidos | **Expectativas claras** e um meio de **responsabilização** |

**Relação**: **SLI → SLO → SLA**. Os SLIs são a base para definir os SLOs, que **informam os SLAs**: medimos com SLIs, definimos **metas internas** com SLOs e fazemos **promessas externas** com SLAs. Ver as Figuras 1 e 2 do PDF.

## Error Budget
- **Conceito fundamental** do **Site Reliability Engineering (SRE)**.
- **Definição**: métrica que define a **quantidade aceitável de tempo** que um serviço pode ficar **indisponível**, geralmente em **porcentagem** ou **tempo de inatividade permitido** num período.
- **Objetivo**: **equilibrar** a necessidade de **lançar recursos e atualizações** com a de **manter a estabilidade e a confiabilidade**.

| | O que o PDF diz |
|---|---|
| **Cálculo** | Com base no **SLA** ou no **SLO** |
| **Uso** | Quando o Error Budget é **consumido**, as equipes **podem ser incentivadas** a focar em **melhorias de estabilidade** em vez de lançar recursos, até o serviço voltar aos níveis acordados |
| **Benefícios** | **Melhoria contínua** (a equipe trabalha proativamente contra a degradação) · **decisão baseada em dados** (base quantitativa para lançamentos, priorização e alocação de recursos) |
| **Desafios** | **Estabelecer SLOs** realistas, que reflitam as expectativas e as capacidades do serviço · **Comunicação** clara entre SRE e desenvolvimento sobre o status do Error Budget e as implicações de excedê-lo |

## Referências
Google: The SRE resource library · What is Site Reliability Engineering (SRE)? · Kumar (2020) · Red Hat: Introdução ao DevOps · O que é SRE?
