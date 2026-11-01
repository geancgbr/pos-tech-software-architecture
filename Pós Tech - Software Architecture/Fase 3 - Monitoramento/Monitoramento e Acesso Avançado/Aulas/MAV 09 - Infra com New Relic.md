---
tags: [pos-tech/fase-3, monitoramento, newrelic, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 9
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 9_rev2.pdf"
---

# MAV 09 - Infra com New Relic

← [[MAV 08 - Logs com New Relic]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 10 - Configurando alertas]]

> [!summary] Em uma frase
> A **infraestrutura no [[New Relic]]**: o **Agent** comunica o host com a plataforma, e as métricas se **correlacionam** com os problemas do APM. O PDF lista **7 boas práticas**: agente em todo o ambiente, integração com o **EC2**, integrações, visualizações de grupos de hosts, alertas por **tags**, infraestrutura junto do APM e dados via **[[NRQL]]**.

## Hands On
Implementar o **agent de infraestrutura** e analisar as métricas coletadas dos hosts.

## As boas práticas
| # | Prática | O que o PDF diz |
|---|---|---|
| 1 | **Instale o agente em todo o ambiente** | A solução é para ambientes **grandes e em constante mudança**, com a UI **orientada por tags**. Instalar em todo o ambiente, até em várias **regiões e clusters**, dá uma imagem mais precisa. Para um **MTTR** mais rápido, instalar em servidores de banco, web e qualquer host que suporte os aplicativos, usando **atributos personalizados** para marcar os hosts. Dá para separar os logs do agente dos logs do sistema. **Como**: módulos para **Chef, Puppet e Ansible**; definir os `custom_attributes`; configurar o atributo `log_file` |
| 2 | **Configure a integração nativa do EC2** | Na AWS, além do agente nas instâncias EC2, a integração **importa automaticamente as tags e os metadados**. Permite filtrar com as tags da AWS (ex.: `ECTag_Role='Kafka'`). Os alertas e filtros são **orientados por tags e dinâmicos**, adicionando e removendo instâncias sozinhos |
| 3 | **Ative as integrações** | O monitoramento vai além de CPU, memória e armazenamento. Integrações prontas: **AWS CloudWatch, AWS Billing, AWS ELB, MySQL, NGINX** e outras, com **painéis pré-configurados** |
| 4 | **Crie visualizações de agrupamentos de hosts** | Com o **filtro de entidade**, salvar visualizações focadas, com o **status de integridade em cores** de cada host |
| 5 | **Crie condições de alerta** | Diretamente no contexto das entidades: em vez de um alerta por host, iniciar a condição **no gráfico da métrica** e com base nas **tags de filtro**. Hosts que ficam offline saem e hosts novos com as tags entram sozinhos; os alertas **escalam para os hosts futuros**. Dá para usar as **políticas de alerta** existentes |
| 6 | **Veja a infraestrutura junto do APM** | Dados do APM e da infraestrutura **lado a lado**, para achar a causa raiz mais rápido. **Mapas de integridade**: as primeiras caixas, a partir do **canto superior esquerdo**, são as que pedem atenção |
| 7 | **Acesse os dados por métricas e eventos** | Um **painel único** que correlaciona infraestrutura com métricas de aplicativos, navegadores e sintéticas. Os dados granulares ficam no New Relic e podem ser consultados com **NRQL** |

## NRQL
- **NRQL** = **linguagem de consulta New Relic**, **semelhante ao ANSI SQL**, para recuperar dados detalhados sobre aplicativos, hosts e atividades de negócio. Ver [[NRQL]].
- **Usos**: criar um **novo gráfico** (Figura 1) · responder a uma **pergunta específica** (solução de problemas ou negócio) · configurar **alertas baseados em NRQL** ("nosso tipo de alerta principal e mais poderoso", diz o texto) · fazer **consultas de API** de dados da New Relic.
- Vai de consultas simples (linhas em formato **tabular bruto**) a **cálculos poderosos** antes de apresentar os dados, como **funis** de interação dos usuários.

## Mantenha tudo atualizado
Um dos pilares das boas práticas: manter os **sistemas e Agents sempre atualizados**, para ter as melhores métricas e funcionalidades.

## Referências
New Relic: Get started with infrastructure monitoring · Get started with NRQL · Guia de práticas recomendadas para monitoramento de infraestrutura · Infrastructure monitoring best practices guide · Positivo (2019)
