---
tags: [pos-tech/fase-3, monitoramento, datadog, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 4
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 4_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 04 - Infra com Datadog

← [[MAV 03 - Logs com Datadog]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 05 - Criando alertas com DD]]

> [!summary] Em uma frase
> A **infraestrutura no [[Datadog]]**: o **Agent** comunica o host com o Datadog e coleta as métricas dos recursos, que se **correlacionam** com os problemas da aplicação. Os destaques são o **Host Map** (cores por estado), a visão de **containers e imagens** e a **integração com a cloud** (catálogo de recursos).

## Hands On
Implementar o **agent de infraestrutura** e analisar as métricas coletadas dos hosts.

## Por que monitorar a infraestrutura
- Monitorar **além de rotas e endpoints**: identificar gargalos e problemas da infraestrutura e correlacioná-los com a performance da aplicação, porque "é impossível ter um problema com **CPU, memória RAM, disco ou rede** e isso não impactar negativamente a aplicação".
- Mesmo com ferramentas open source como **Grafana, Prometheus e Zabbix**, muitas empresas adotam a prática de **All-in-One**, ainda que custe um pouco mais.

## Host Map
Um **mapa lógico e macro** de cada host monitorado (Figura 1):

| Cor | Significado |
|---|---|
| **Cinza** | **Perda de comunicação** com o host |
| **Vermelho** | Problema com a **CPU** do host |
| **Laranja** | Problema de **desempenho** no host |
| **Verde** | Comunicação e desempenho **ok** |

- Em cada host é possível dar **zoom**: serviços instalados, integrações e métricas detalhadas de cada aplicação (Figura 2).

## Casos de uso
**Otimização de recursos (AWS)**
- Para reduzir gastos, descobrir para que servem as instâncias caras: agrupar por **instance type** e depois por **role** ou **name**. Há funções de host com **CPU subutilizada**? Ampliar os hosts e ver se precisaram de todo aquele poder nos últimos meses, ou se são candidatos a um **tipo de instância mais barato**.
- **Exemplo da Figura 3**: hosts (hexágonos) agrupados por tipo: **m3.large**, **c3.2xlarge** e **m1.xlarge**. Os m3.large e m1.xlarge estão quase todos **verdes** (baixa utilização de CPU); os **c3.2xlarge** estão **laranja** (alta utilização). Agrupando o c3.2xlarge por função, só algumas estão carregadas. O **downgrade de 7 nós verdes para c3.xlarge** economizaria **quase US$ 13 mil por ano** (US$ 0,21/hora/host × 24 h × 365 dias × 7 hosts = **US$ 12.877,20/ano**).

> [!note] Na legenda geral, o verde é "comunicação e desempenho ok"; no exemplo da Figura 3, verde e laranja indicam baixa e alta utilização de CPU, embora a legenda atribua o problema de CPU ao **vermelho** e o de desempenho ao laranja.

**Investigação de problemas**
- Quando não se acha o causador de um problema na aplicação, ainda dá para analisar a infraestrutura (CPU, RAM). As instâncias se comunicam e podem causar atrasos e **lentidão generalizada**; com o Host Map, dá para analisar essa comunicação e medir memória e CPU, **no mesmo cluster ou não**.

## Containers e imagens
- Análise e visualização de **containers** em **AWS ECS, EKS ou Azure**, Docker e Kubernetes, com a **lista completa de containers** e filtros por **Namespaces, services, pods e configurações**.
- A partir da orquestração, analisar as **imagens** usadas pelos containers, chegando a um nível superior que analisa até **vulnerabilidades** das imagens (Figura 4).

## Integração com a cloud
- Fora do agente, a **integração com uma cloud** traz **todos os recursos criados na nuvem** (bancos, lambdas, rede, segurança), escolhidos numa lista. Aplica-se às **principais clouds**, e **toda integração é cobrada por ingest** (armazenamento usado e coletado da cloud). Figura 5.
- **Catálogo de recursos**: as pessoas responsáveis analisam os recursos **sem precisar de acesso à cloud** (onde poderiam fazer alterações e causar danos), garantindo a **cobertura de segurança**, a visão do cenário inteiro, insights de melhoria e um **inventário** para consultas.

## Referências
Datadog: AWS Integration · Container Images View · Datadog Resource Catalog · Host and Container Maps · Infrastructure · Welcome to Datadog Docs!
