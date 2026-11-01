---
tags: [pos-tech/fase-4, resiliencia, microsservicos, aula]
disciplina: Resiliência em Microsserviços
aula: 1
fonte: "Resiliência em microservices/Aula 01 - Introdução a resiliência.pdf"
---

# RES 01 - Introdução à resiliência

[[Resiliência em Microsserviços]] · Próxima → [[RES 02 - Padrões de resiliência]]

> [!summary] Em uma frase
> **Resiliência** é a capacidade de sistemas, processos e componentes **suportarem falhas mantendo a operação**, total ou parcial. É um **requisito crítico**. A aula distingue **defeito, erro e falha**, os tipos de defeito (**inconsistentes**, como os bizantinos, **consistentes** e **fail-stop**), as métricas (**taxa de erros, coverage, reliability, MTTF, MTTR, MTBF, availability**), o **mindset de resiliência** e a base de tudo: **balanceamento de carga, health checks e escalabilidade horizontal**. Ver [[Resiliência]].

## Hands On (vídeos)
Nas videoaulas: o conceito de resiliência e **por que se preocupar com falhas** (de software, hardware, redes e bugs inesperados), com dicas e estratégias práticas.

## O que é resiliência
- A capacidade de **sistemas, processos e componentes** suportarem uma ampla variedade de **falhas**, mantendo a operação **total ou parcial**.
- Quando um serviço falha, ele deve ter **métodos para lidar** com a situação e **reduzir o efeito** no desempenho geral. "Tudo o que é desenvolvido e implementado com a devida qualidade **pode ser** uma prática de resiliência."
- O software está **mais complexo** (expectativas crescentes, sistemas integrados, cargas em escala sem precedentes, prazos mais curtos) e **essencial**: quando falha, processos param e, em casos extremos, **vidas podem estar em risco** (ex.: um sistema de UTI indisponível). Por isso a resiliência é um **requisito crítico**.

## Defeito, erro e falha
| Termo | O que é (segundo o PDF) | Exemplos |
|---|---|---|
| **Defeito** | O software **não opera conforme as especificações** (funcionalidades, restrições, qualidade). Percebido por usuários ou monitoramento. **Todo defeito é causado por um erro** | Crashes inesperados, resultados incorretos, indisponibilidades |
| **Erro** | Um **comportamento inadequado** que **pode** originar um defeito: valores incorretos gerados ou armazenados, ou **tempo excessivo**. A arquitetura deve identificá-lo **o mais cedo possível** | Race conditions e **timeouts**, loops infinitos, violação de protocolos (formato, sequência, pré e pós-condições, invariantes), inconsistência de dados, não suportar a carga |
| **Falha** | A **causa raiz** de um erro: uma imperfeição no design, na implementação ou na operação (código, configuração, hardware, processos humanos). Cria as **condições** para erros e defeitos | Bugs, configuração incorreta, defeitos de hardware, problemas de rede, equívocos de operadores |

> [!note] Na lista do PDF, "defeito" é **fault** e "falha" é **failure**; nos títulos das seções, os termos aparecem trocados: "Defeitos (**Failures**)" e "Falhas (**Faults**)".

## Três tipos de defeitos
| Tipo | Como se comporta | Como lidar |
|---|---|---|
| **Inconsistentes** | O comportamento varia conforme o **momento ou quem observa**. Exemplo clássico: as **Byzantine Failures**, em que partes do sistema enviam informações **corretas para alguns nós e incorretas para outros** | Estratégias sofisticadas: **clusters com protocolos de consenso**, como **Paxos** ou **Raft**, para os nós "saudáveis" chegarem a um acordo |
| **Consistentes** | Sempre se manifestam **da mesma forma**: previsíveis, mais fáceis de detectar | Normalmente **2n+1 réplicas** (n = falhas toleradas), para haver **votos** suficientes |
| **Fail-stop** | O componente **para completamente** (como num crash), sem gerar resultados incorretos | Normalmente **n+1 réplicas**; mais simples |

- Uma falha é **"silenciosa"** quando não impede o componente de produzir resultados corretos ou, no extremo oposto, quando o impede **completamente**. O **fail-stop** se baseia nesse comportamento: é fácil detectar que o componente parou.

## Métricas de resiliência
- **Resiliência × disponibilidade**: relacionadas, mas **não são a mesma coisa**. A **disponibilidade** pode medir a proporção de **solicitações processadas com sucesso** ou o **tempo funcional** sobre o período total. A **resiliência** não é **apenas** um indicador, mas um **conjunto de estratégias e mecanismos** para manter a disponibilidade diante de falhas.
- **Taxa de erros** (a métrica mais comum, baseada no uso real): erros ÷ total de requisições. **Exemplo**: 1.000 requisições em 1 hora, **40** erros do servidor → **4%** de erros, **96%** atendidas. Daí vem a **disponibilidade de uso**.

| Métrica | O que mede |
|---|---|
| **Coverage Factor** (índice de cobertura) | A probabilidade de **detectar** uma falha e **se recuperar automaticamente** em tempo aceitável |
| **Reliability** (confiabilidade) | A probabilidade de produzir **resultados corretos** e se comportar conforme especificado; ligada ao tempo **sem falhas** |
| **Availability** (disponibilidade) | A proporção de tempo em que o sistema está **acessível e funcional**; depende também dos **mecanismos de recuperação** |

**Métricas de confiabilidade** (Figura 1)
| Métrica | Definição | Exemplo do PDF |
|---|---|---|
| **MTTF** (Mean Time to Failure) | Tempo médio de funcionamento **antes** de um problema | 10 lâmpadas que duram 1.000 h em média → MTTF de **1.000 h** |
| **MTTR** (Mean Time to Repair) | Tempo médio para **recuperar** depois da falha; quanto menor, melhor | Reparos de 2, 3 e 1 h em 3 falhas → **2 h** |
| **MTBF** (Mean Time Between Failures) | Intervalo médio **entre duas falhas**: **MTTF + MTTR**; quanto maior, mais confiável | MTTF de 900 h + MTTR de 100 h → **1.000 h** |

- **Dica**: comparar o MTBF entre equipamentos ou períodos, para ver melhorias e justificar manutenção preventiva.

## Mindset de resiliência
- Questionar sempre: **"O que pode dar errado com esta decisão ou implementação?"**, do planejamento à operação.
- **Exemplo**: um e-commerce é **defeituoso** se não registra pedidos corretamente; os **erros** são pedidos com itens não solicitados ou sem os comprados; por trás, **falhas** como integração com o estoque, lógica de negócio ou comunicação entre serviços.

| Prática | O que o PDF diz |
|---|---|
| **Programação defensiva** | Validar entradas, tratar exceções, evitar a propagação de pequenos erros; padrões como **circuit breaker** e **retry policies** |
| **Chaos engineering** | Cenários **controlados** de falha (desligar instâncias, induzir lentidão, falhas de rede) para testar a recuperação. Ver [[Chaos Engineering]] |
| **Testes automatizados** | Unitários, de integração, de contrato e de carga |
| **Redundância** | **Failover** e **balanceamento de carga** para componentes críticos |
| **Monitoramento contínuo** | Métricas, alertas e dashboards, com resposta automática (escalar recursos, reiniciar serviços) |

## A base: balanceamento e escalabilidade horizontal
- "A principal e mais simples estratégia de resiliência" é revisitar **distribuição e balanceamento de carga** e **escalabilidade horizontal**, com **auto-scaling** para adicionar e remover réplicas sob demanda.
- As aplicações devem expor **URLs de health check** que reflitam seu estado por **códigos de resposta** monitorados periodicamente (Figura 2). `/api/health` é **só um exemplo**: não existe caminho padrão.
- Os **balanceadores**: distribuem as requisições; fazem **health checks periódicos**, retirando do pool as réplicas com erros recorrentes ou sem resposta no tempo limite; garantem o **paralelismo externo** de requisições síncronas; e, com **auto-scaling**, reagem às variações de carga.

## Mercado, cases e tendências
Livros indicados: *Designing Data-Intensive Applications* (Martin Kleppmann) · *Distributed Systems: Principles and Paradigms* (Tanenbaum e van Steen) · *Site Reliability Engineering* (Google).

> [!note] As recomendações de livros falam em "erros/defeitos **consistentes**" com replicação e **consenso**; no corpo da aula, o consenso (Paxos/Raft) é a solução para defeitos **inconsistentes**, e os consistentes usam 2n+1 réplicas.

## Referências
GeeksforGeeks: Architecture styles in distributed systems · Beyer et al., *Site Reliability Engineering* · eMaint: MTTF · Fowler, *Patterns of Enterprise Application Architecture* · Fox e Brewer: Harvest, yield, and scalable tolerant systems · Kleppmann · Microsoft: Verificar integridade de instâncias no Azure App Service
