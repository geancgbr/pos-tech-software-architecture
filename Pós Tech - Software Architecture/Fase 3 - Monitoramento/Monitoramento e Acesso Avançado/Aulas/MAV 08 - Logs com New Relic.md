---
tags: [pos-tech/fase-3, monitoramento, newrelic, logs, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 8
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 8_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 08 - Logs com New Relic

← [[MAV 07 - Introdução APM New Relic]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 09 - Infra com New Relic]]

> [!summary] Em uma frase
> Os **[[Logs in Context]]** do **[[New Relic]]** mostram os logs **no contexto** de outras telas da plataforma (APM, infraestrutura, distributed tracing, Errors Inbox), para chegar à **causa raiz** mais rápido. No .NET há **três opções**: encaminhamento pelo agente, **log decoration** com um encaminhador externo e envio manual dos metadados (não mais incentivado).

## Hands On
Instrumentar os logs das aplicações que já tinham **APM no New Relic** e analisar os logs enviados com **Logs in Context**. Segundo o "O que vem por aí", também se veem **Drop Rules** e **Patterns**, e a instrumentação em **.NET e NodeJS**.

## Logs in Context
- Disponível ao relatar logs pelo **APM agent**, pelo **agent de infraestrutura** ou pela **integração OpenTelemetry**.
- Mostra os dados de log em telas como **APM, monitoramento de infraestrutura, distributed tracing e Errors Inbox**, sem pesquisar os logs manualmente. Reunir os dados de aplicativos e infraestrutura **numa única solução** ajuda a chegar à **causa raiz** mais rápido e a ver padrões e tendências.
- **Habilitados por padrão** no APM (na opção 1, o PDF diz que isso vale a partir do agente 9.8.0). Segundo o PDF, isso **pode** ter impacto negativo na **segurança, conformidade, faturamento ou desempenho**.

**Limitações conhecidas (segundo o PDF)**
- Exceto no agente **Node.js**, o **APM logs forward não envia o log completo**. O **log de inicialização** só fica disponível depois que o agente carrega.
- No **Kubernetes**, o log é decorado **via instrumentação**, não pela API do Kubernetes; o log nunca toca o host.
- Quando uma exceção é lançada, o **stack trace** não aparece nos logs contextualizados dos agentes **Java ou .NET**. Alternativa: alterar as **regras do filtro de descarte**.
- O **Fluentd** pode adicionar o **processID**, mas o log do APM não vê isso; os metadados do Kubernetes também não aparecem no aplicativo. Se precisar deles, use os logs contextualizados automáticos **sem enviar o log do aplicativo**, e continue com **Fluentd, Fluent Bit** ou outra solução para encaminhar o arquivo de log.

## As três opções no .NET
Há requisitos mínimos para coletar o log **sem um agente específico** de encaminhamento (estrutura suportada na Figura 1). O **Sitecore.Logging** (baseado num fork do log4net) é suportado desde o agente .NET **10.14.0**.

| # | Opção | O que o PDF diz |
|---|---|---|
| 1 | **Encaminhamento pelo agente** (a mais simples) | Para quem não tem acesso ou interesse em configurar um direcionador de logs. O registro inclui **`span.id`, `trace.id`, `hostname`, `entity.guid` e `entity.name`**. Basta um agente com encaminhamento (**.NET 9.7.0 ou superior**); se estiver desabilitado, habilita-se no arquivo de configuração (Figuras 2 e 3). Desde o **9.8.0**, vem habilitado por padrão |
| 2 | **Log decoration com um encaminhador externo** | O agente **decora** o log com os metadados de link. **Não usar junto com o encaminhamento no agente**: o log seria enviado **duas vezes**, o que pode gerar **cobrança dupla**. A decoração adiciona **cinco atributos**: `entity.guid`, `entity.name`, `hostname`, `trace.id` e `span.id` |
| 3 | **Atualizar o aplicativo para enviar os metadados de link** | **Ainda suportada, mas não é mais incentivada**. Exige um **direcionador de logs** antes; sem ele, a interface indica um **agente de infraestrutura**. Ao migrar depois para os logs automáticos, **desabilite o forwarder manual**, senão as linhas vão duplicadas (cobrança dupla) |

## Caso de uso (do artigo da New Relic)
1. Um engenheiro de plantão recebe um **alerta** de tempo de resposta insatisfatório e erros crescentes. Precisa decidir se **tira um host do balanceamento** ou **reverte a última versão**.
2. Na página **Summary do APM**, vê muito mais **logs de erro**, que levam ao aumento do tempo de resposta (Figura 5). A coleta de logs não estava configurada, mas o **agente Java** foi atualizado para incluir **logs de APM no contexto**, então os logs chegam automaticamente, com contagem por **gravidade**.
3. No gráfico **Logs**, abre o **Log Summary**: quando os logs foram coletados, os de severidade **Error ou pior** e a lista de **padrões** com a porcentagem de cada um.
4. Em **Log Patterns**, mensagens de erro **raras** passaram a ser **frequentes**, o que o ajuda a focar no log problemático em vez das atualizações **"noisy"** (Figura 6).
5. Em **Log Details**, vê todos os valores do registro e pode ir ao **Kubernetes**, ao **distributed tracing** ou aos erros do APM (Figura 7). No erro do APM, vê o **stack trace** e o registro no **Errors Inbox** (Figura 8).
6. A equipe descobre que o problema veio de uma **alteração recente** e **reverte o código**. Para economizar, recusa a coleta de log em `application_logging:forwarding:max_samples_stored:`, mas mantém a **amostragem**. Atualiza os **runbooks** para apontar para a página Log Patterns filtrada e os vincula à condição do alerta.

## Referências
Google: The SRE resource library · New Relic: Logs contextualizados APM · Red Hat: Introdução ao DevOps · O que é o kernel Linux?
