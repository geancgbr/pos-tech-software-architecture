---
tags: [pos-tech/fase-3, monitoramento, sre, conceito]
aliases: [Orçamento de erro, error budget]
---

# Error Budget

**Conceito fundamental do SRE**: a **quantidade aceitável de tempo** que um serviço pode ficar **indisponível**, geralmente em porcentagem ou tempo de inatividade permitido num período. Equilibra **lançar recursos e atualizações** com **manter estabilidade e confiabilidade**.

- **Cálculo**: com base no **SLA** ou no **SLO** ([[SLI, SLO e SLA]]).
- **Uso**: consumido o Error Budget, as equipes **podem ser incentivadas** a focar em **estabilidade** em vez de novos recursos, até voltar aos níveis acordados.
- **Benefícios**: melhoria contínua; decisões baseadas em dados (lançamentos, priorização, alocação).
- **Desafios**: estabelecer SLOs realistas; comunicação clara entre SRE e desenvolvimento.
- **Em alertas**: alertar pela **queima do error budget** foca no que impacta os compromissos com os usuários ([[MAV 05 - Criando alertas com DD]]).

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
**Error Budget = 100% − SLO** (ex.: 98% de disponibilidade → 2%). No exemplo financeiro, 10.000 pedidos por semana, tolerância de 1% (SLO 99%) e R$ 10,00 de prejuízo por pedido ruim dão um budget de R$ 1.000,00 ([[MS2 06 - Realizando o deploy de microsserviços, parte 2]]).

## Na disciplina Resiliência em Microsserviços (Fase 4)
MTBF, MTTR, **SLOs** e **Error Budget** estão entre as métricas para medir o sucesso de um programa de [[Chaos Engineering]] ([[RES 05 - Chaos Engineering]]).

Aparece em: [[MAV 01 - O que é APM e seus benefícios]], [[MAV 05 - Criando alertas com DD]], [[MS2 06 - Realizando o deploy de microsserviços, parte 2]], [[RES 05 - Chaos Engineering]]
