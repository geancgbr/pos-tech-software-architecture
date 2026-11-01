---
tags: [pos-tech/fase-4, microsservicos, observabilidade, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 6
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 6.pdf"
---

# MS2 06 - Realizando o deploy de microsserviços, parte 2

← [[MS2 05 - Realizando o deploy de microsserviços]] · [[Estrutura de Microsserviços Parte II]]

> [!summary] Em uma frase
> **Instrumentar os serviços** para observar o comportamento em sucesso e em falha. O Hands On monta **Elasticsearch, Logstash e Kibana**. O texto do PDF trata de **alertas e notificações** (warning × alert), do **[[OpenTelemetry]]** e de **[[SLI, SLO e SLA]]** com o **[[Error Budget]]**.

## Hands On
Repositório da aula 6 e **Postman**. Instanciar o **Elasticsearch** para o envio de logs, configurar o **Logstash** para **transformar** os logs antes de indexá-los e configurar o índice no **Kibana**, com gráficos e **dashboard**. Ver [[EFK (Elasticsearch, Fluentd e Kibana)]].

**Segundo o resumo**: **métricas, logs e traces** e a utilidade de cada um; o **trace distribuído** (visão de ponta a ponta, causa raiz); **health check**; **agregação de logs** num servidor central; **logs de auditoria** (atividades suspeitas de usuários); e o mapeamento de **exceções não previstas**.

## Alertas e notificações
- A instrumentação gera muitos dados; é essencial **reagir em tempo real**.
- **Alertas**: eventos gerados quando uma métrica atinge um **limite**. **Notificações**: mensagens às equipes (e-mail, SMS, Slack, Teams). Permitem agir rápido e até **antes** do problema.

| Passo | O que o PDF diz |
|---|---|
| **Ferramenta** | Open source, como **Prometheus com Alertmanager**, ou pagas, como **Datadog, Dynatrace, New Relic, AppDynamics, Splunk** |
| **Métricas** | As vitais para o serviço e o ponto em que indicam problema; as ferramentas de mercado permitem, inclusive, gerar métricas a partir de traces e logs |
| **Thresholds** | Valores **realistas**. Um de **aviso (warning)** ("algo pode estar errado") e outro de **alerta (alert)** ("algo definitivamente deu errado"); o aviso dá tempo ao time de sustentação |
| **Mensagem** | Informações suficientes para a equipe entender e reagir; **normalmente** **título, descrição e criticidade** |
| **Canais** | Slack, e-mail, Teams, SMS, webhook; **reenviar** se persistir (ex.: a cada **30 minutos**) |
| **Testar** | Sempre testar os alertas |

- **Melhores práticas**: **não sobrecarregar** (fadiga, falsos positivos; revisar os thresholds) · **ser específico**, direcionando ao público certo com **tags** (ex.: **"#dba"**) · **documentar** o significado e a resolução de cada alerta. Ver [[Monitors do Datadog]].

## OpenTelemetry
- Projeto de **observabilidade de código aberto** da **CNCF**, com **APIs, bibliotecas e agentes** para coletar **traces e métricas distribuídas**. Combina o melhor de **OpenTracing** e **OpenCensus**.
- Torna mais fácil para as pessoas desenvolvedoras **instrumentarem** os serviços, **independente de tecnologia**, e integra com qualquer solução compatível com o **OTLP**.
- **Como usar**: **instalação** (bibliotecas e SDKs) · **configuração** (o que coletar) · **exportação** (ex.: **Prometheus** para métricas, **Jaeger** para traces).
- **Melhores práticas**: **dados contextuais** (ex.: SKU, cor e tipo no trace de produto, para buscar traces do tipo **"Lâmpada"**) · **padrões de nomenclatura** (ex.: um campo `endpoint: produto` para filtros, gráficos e alertas) · **amostragem** (ex.: **50%**, para reduzir custos com licenças, ainda com visão estatística). Ver [[Amostragem (Sampling)]].

> [!note] Aqui o PDF descreve o OpenTelemetry como fornecedor de APIs, bibliotecas e agentes **para coletar traces e métricas**; na disciplina OpenTelemetry (Fase 2), ele também cobre **logs**.

## SLI, SLO e SLA
| | Definição | Exemplo do PDF |
|---|---|---|
| **SLI** | Métricas ou indicadores da **qualidade** do serviço | Tempo de resposta, taxa de erro |
| **SLO** | **Metas ou limites** para os SLIs | Nos últimos **7 dias**, **95%** das requisições com resposta **< 2 s** |
| **SLA** | **Contrato formal** com os clientes, **normalmente baseado nos SLOs** | **90%** das operações do mês em até **2 s** |

- Dão uma **compreensão objetiva** do esperado, permitindo que as equipes **priorizem** trabalho e recursos; o **valor de cada serviço** para o negócio é entendido através dos **SLOs** definidos.
- **Como usar**: identificar os SLIs → definir SLOs **realistas, mas desafiadores** → **monitorar os SLIs** e configurar **alertas baseados nos SLOs** → formalizar num SLA, se aplicável.
- **Melhores práticas**: **revisão periódica** · **equilíbrio** (nem impossíveis, nem frouxos) · **transparência**.

## Error Budget
- **Está relacionado com** a **margem de falhas** que o negócio tolera em cada operação; **podemos modelar um SLO** a partir dele: **Error Budget = 100% − SLO**.
- **Exemplos**: **98%** de disponibilidade em 12 meses → budget de **2%**; **90%** dos pedidos com resposta < 5 s em 30 dias → **10%**.
- **Exemplo financeiro**: um SLI considera "bom" um pedido **sem falha e com resposta < 15 s**. Com **10.000 pedidos por semana** e tolerância de **1%** (SLO de **99%**), são **100 pedidos ruins**; a **R$ 10,00** de prejuízo cada, o budget financeiro é de **R$ 1.000,00** ("por exemplo, por mês", diz o PDF). Se o SLI cair para **98%**, consome-se todo o budget (1%) e mais **1%** adicional, **2%** no total.

> [!note] No exemplo financeiro, os pedidos são contados **por semana**, mas o budget de R$ 1.000,00 é dado "por exemplo, por mês".

> [!warning] O título da aula é "Realizando o deploy de microsserviços - Parte 2", mas o conteúdo não trata de deploy: é todo de observabilidade (instrumentação, ELK, alertas, OpenTelemetry, SLI/SLO e Error Budget).

## Referências
Richardson, *Microservices Patterns* · Richardson: Application metrics · Audit logging · Distributed tracing · Exception tracking · Health Check API · Log aggregation · Log deployments and changes
