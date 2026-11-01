---
tags: [pos-tech/fase-3, monitoramento, datadog, alertas, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 5
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 5_rev2.pdf"
---

# MAV 05 - Criando alertas com DD

← [[MAV 04 - Infra com Datadog]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 06 - Criando dashboards com DD]]

> [!summary] Em uma frase
> O **alerta proativo** é um pilar da observabilidade: reduz o **MTTD** e o **MTTR**. No **[[Datadog]]**, os **Monitors** são o coração do alerting: regras que, atendidas, disparam um alerta. Um monitor tem **método de detecção, métrica/query, condições, notificação, renotificação, agrupamento e permissões**. Bons alertas são **acionáveis**, evitam a **fadiga de alerta** e usam os **SLOs** como guia. Ver [[Monitors do Datadog]].

## Hands On
Navegar pela seção **"Monitors"**, criar o primeiro **monitor de métrica** do zero (métrica, limiares de **alerta e aviso**, notificações) e configurar **monitores de APM** para **latência e taxa de erros**.

## Por que o alerta proativo
- Em sistemas **complexos e distribuídos** (microsserviços), detectar e reagir rápido é **necessidade fundamental**. Esperar o usuário reclamar ou alguém notar num dashboard visto de vez em quando é uma estratégia **reativa e arriscada**: o custo vai de **perda de receita e dados** a **danos à reputação**.
- Um sistema de alerting bem configurado é uma **"sentinela vigilante"**: identifica desvios, erros ou degradação e notifica as equipes de forma **imediata e contextualizada**.

| Benefício | O que o PDF diz |
|---|---|
| **Menor MTTD** (Mean Time To Detect) | Alertas automáticos detectam muito mais rápido que a detecção manual |
| **Menor MTTR** (Mean Time To Resolve) | Detecção rápida e notificações com contexto adiantam a investigação e a correção |
| **Experiência do usuário** | Resolver antes que afete muita gente, ou mitigar rápido |
| **Eficiência operacional** | Menos "apagar incêndios" e menos olhar dashboards manualmente |
| **Prevenção de perdas financeiras** | Menos downtime e degradação = menos perda de negócio |

## Anatomia de um monitor
**1. Método de detecção (Detection Method)**
| Método | Como funciona | Quando usar / observação |
|---|---|---|
| **Threshold** (limiar) | Alerta se o valor cruza um **limiar estático** por um período | **Ideal** para métricas com limites bem conhecidos (disco > 90%, erro > 5%) |
| **Anomaly** (anomalia) | **Machine learning** aprende o normal (incluindo **sazonalidades** diárias ou semanais) e alerta em desvios. **Requer período de aprendizado** | **Útil** para métricas cujo "normal" varia ou é difícil fixar |
| **Forecast** (previsão) | ML **projeta valores futuros** e alerta se um limiar **será cruzado** em breve (ex.: disco cheio em 24 h) | Permite uma ação ainda mais proativa |
| **Outlier** (discrepante) | Monitora um **grupo de itens semelhantes** e alerta se um ou mais se comportarem diferente dos demais | O grupo pode ser, por exemplo, todos os hosts de um cluster ou todos os containers de um serviço |

**2. Métrica ou consulta (Define the metric/query)**: o **"o quê"** do alerta.
- **Métrica**: ex. `system.cpu.user`, `nginx.requests.per.second`, `trace.flask.request.duration.p95`, com **agregações** (avg, sum, min, max, count), **agrupamentos** (by host, service, region) e **transformações** (`as_rate()`, `as_count()`). É fundamental usar **tags** para escopar (ex.: `env:prod AND service:api-pagamentos`).
- **Log**: uma query de busca; o alerta se baseia na **contagem de logs** que casam num intervalo.
- **APM**: serviço, **resource** (endpoint) e uma métrica como **latência (p50 a p99)** ou **taxa de erro**.

**3. Condições de alerta (Set alert conditions)**
- **Limiares**: estados **"Alert"** (crítico) e, opcionalmente, **"Warning"** (ex.: alerta acima de 100, aviso acima de 80).
- **Janela de avaliação**: por quanto tempo a condição deve valer (ex.: "over the last 5 minutes"), para evitar alertas por **flutuações momentâneas**.
- **"No Data"**: alertar se a métrica **parar de reportar** (pode ser problema no agente ou na aplicação).
- **Auto-resolve**: resolver sozinho quando a condição deixar de valer.

**4. Notificações e mensagem (Say what's happening and notify your team)**
- **Título** conciso, com **variáveis de template** (ex.: `CPU alta no host {{host.name}}`).
- **Corpo** com contexto: `{{value}}`, `{{threshold}}`, `{{service.name}}`, links para dashboards ou **runbooks**.
- **Destinatários**: e-mail, Slack, PagerDuty, Microsoft Teams, webhooks e outros, com **@-mentions** (ex.: `@slack-canal-equipe-backend`).

**5. Renotificação**: reenviar se o alerta continuar ativo. **6. Agrupamento**: por padrão, um alerta por fonte (ex.: um por host); ou um **multi-alert** que resume todos. **7. Permissões e salvamento**: quem pode editar; ao salvar, o monitor começa a operar.

## Tipos de monitores
| Tipo | Para quê | Exemplo do PDF |
|---|---|---|
| **Metric Monitors** ("espinha dorsal") | Infraestrutura, aplicações, serviços gerenciados e métricas customizadas | CPU média dos servidores web de produção > 80% por mais de 10 min; p99 de uma métrica de pagamento > 500 ms |
| **APM Monitors** | **Trace & Span Analytics** (latência, erro, requests) · **Error Tracking** (agrupa erros similares e pode alertar sobre novos tipos ou aumento) · **SLOs** (metas como 99,9% de sucesso e alerta sobre o **error budget** consumido) | p95 de `/api/checkout` > 300 ms por 5 min; erro do `servico-de-usuarios` > 1% em 15 min |
| **Log Monitors** | Contagem de logs que casam com uma query: picos de erros, acessos não autorizados, eventos críticos | Mais de 10 logs com "Null Pointer Exception" do `servico-catalogo` em produção em 5 min |
| **Synthetic Monitors** | **API Tests** (disponibilidade, tempo e correção da resposta) e **Browser Tests** (jornadas de usuário num navegador real) | `/health` sem 200 OK em 3 tentativas de locais diferentes; falha na jornada de login |
| **Composite Monitors** | Combinam monitores com **AND, OR, NOT**, para **reduzir ruído** | "Alertar SOMENTE SE (o monitor de CPU alta estiver ativo); (o monitor de alta latência no serviço X estiver ativo)" |

## Melhores práticas
- **Alertas acionáveis**: cada alerta deve ter uma **ação clara**, idealmente com um **runbook** (manual de procedimento). "O que eu espero que alguém faça com esta informação?"
- **Evite a fadiga de alerta**: muitos falsos positivos ou alertas de baixa prioridade fazem as pessoas ignorá-los. **Ajuste os thresholds** (Warning × Alert), use **janelas apropriadas**, **não alerte sobre tudo** ("monitore muitas coisas, mas alerte seletivamente") e **priorize** os sistemas críticos.
- **Contexto**: o que está errado, o que foi afetado, valor e limiar, período, links para dashboards e runbooks.
- **Revisão e iteração**: revisar regularmente, analisar alertas passados (úteis? falsos positivos?), ajustar e **coletar feedback** da equipe.
- **SLOs como guia**: alertar pela **queima do error budget** foca no que impacta os compromissos com os usuários. Ver [[Error Budget]].
- **Documente**: por que o alerta existe, o que significa, o impacto e os passos de investigação.

## Referências
Datadog: Getting started with Monitors · Monitor Types · Variables
