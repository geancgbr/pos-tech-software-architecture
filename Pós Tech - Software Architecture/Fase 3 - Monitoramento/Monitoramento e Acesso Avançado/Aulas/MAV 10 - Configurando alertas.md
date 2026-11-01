---
tags: [pos-tech/fase-3, monitoramento, alertas, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 10
fonte: "Monitoramento e Acesso Avançado/10SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 10_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 10 - Configurando alertas

← [[MAV 09 - Infra com New Relic]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 11 - Criando dashboards com New Relic]]

> [!summary] Em uma frase
> Alertas no **Datadog** e no **New Relic**, baseados em **regras de negócio**, para um **monitoramento ativo**, sem esperar o cliente avisar. Nos conceitos de alerta (Figura 1, fonte New Relic), uma **política de alerta** reúne **condições** com limites; violado o limite, nasce um **incidente**, e um **Workflow** notifica. O PDF lista **7 boas práticas**, de nomes claros a **automatizar a criação de alertas com Terraform**.

## Hands On
Criar alertas com **Datadog e New Relic**, fazer alguns **disparos**, ver como cada alerta chega e **melhorá-los** com mais detalhes dos problemas.

## Conceitos e termos de alerta (Figura 1, fonte New Relic)
- Um **incidente** é gerado quando o **limite de uma condição de alerta** ativa é atingido. Incidentes semelhantes podem ser **correlacionados**, e as condições podem ser **agrupadas** numa **política de alerta**.
- **Workflows**: configuram as **notificações**, que podem ir para **vários canais**, para alcançar o grupo certo de pessoas e ajudar na **triagem**.
- **Como funcionam** (Figura 1): uma **política** inclui uma ou várias **condições**, cada uma com um **limite**. Violado o limite, um **incidente** é acionado. Com um **fluxo de trabalho**, você é **notificado**. Segundo o PDF, dá para agrupar **incidentes em problemas** e **problemas em decisões**.
- Com o **NRQL**, criam-se condições focadas no que mais importa ([[NRQL]]).

## Boas práticas
| # | Prática | O que o PDF diz |
|---|---|---|
| 1 | **Nomenclaturas claras** | O nome deve informar logo de cara. `INSTANCIA01-CPU` não diz nada; `AWS-Instancia01-Prod-SP-CPU-Critical` ou `AWS-RDS-Sonar-Prod-SP-Lock-Table` dizem **conta, região, serviço e causa aparente**. **Tags** nas condições permitem filtros flexíveis nos workflows ou podem ser adicionadas à notificação |
| 2 | **Categorize as condições** | Categorias, expectativas e um **destino exclusivo** por categoria. Ex.: **proativos** no **Slack** (antes do incidente), **reativos** no **PagerDuty** (incidente em andamento) e **informativos** no **Jira**. Definir o **método de comunicação e escalonamento** (e-mail, SMS, WhatsApp, Slack, Jira, Teams, PagerDuty) para avisar **de forma ativa** |
| 3 | **Times de primeiro atendimento** | A **agilidade** no tratamento faz diferença. Exemplo: um **banco enorme** sem time de primeiro atendimento teria quedas constantes, e os clientes trocariam de banco |
| 4 | **Runbooks** | Ver abaixo |
| 5 | **Revisão mensal dos alertas** (no corpo, "revisões periódicas") | Conferir se os valores ainda fazem sentido. Senão, vira **spam** e as pessoas param de dar atenção |
| 6 | **Métricas de SRE** | **SLIs** para monitorar continuamente e achar problemas antes dos usuários; **SLOs** como metas quantitativas (disponibilidade, tempo de resposta), baseadas nas necessidades dos clientes (Figura 2). Ver [[SLI, SLO e SLA]] |
| 7 | **Automatize com Terraform** | Evita **alterações não documentadas**, dá **rastreabilidade** e **padronização**, e cria uma **documentação rica** dos alertas. Ver [[Terraform]] |

## Runbook
- Um **conjunto de procedimentos** criado por gestores departamentais, principalmente de TI, para definir e manter uma **rotina de trabalho** e garantir que operações **manuais e automáticas** sejam sempre **padronizadas**. "Uma espécie de **manual de procedimentos**".
- Contém: **quem** faz cada tarefa · **quais ferramentas e métodos** · **quais recursos** · qual o **"time"** (prazo) · **como lidar com os problemas mais comuns**.
- Exemplos de procedimentos: **iniciar e parar um sistema**, manipular dispositivos especiais (montagem de racks), **programar backups**.
- Também é um documento com os **itens a monitorar** e as **tarefas operacionais regulares**: um roteiro claro e sistemático para monitorar, controlar e manter os sistemas.

## Referências
Datadog: Monitors · Google: The SRE resource library · New Relic: Introduction to alerts
