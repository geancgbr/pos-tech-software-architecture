---
tags: [pos-tech/fase-2, kubernetes, observabilidade, conceito]
aliases: [EFK, Elasticsearch, Fluentd, Kibana, Fluent Bit]
---

# EFK (Elasticsearch, Fluentd e Kibana)

Pilha para **coletar, processar e visualizar logs** num ambiente Kubernetes. O mecanismo nativo de logs do Kubernetes **não basta**, porque os logs precisam de um ciclo de vida **independente dos Pods e contêineres** (por exemplo, para ler logs de Pods finalizados por erro ou excluídos).

| Componente | O que é | Papel |
|---|---|---|
| **Fluentd** | Coletor de logs de código aberto (arquivos, stdout, syslog) | **Componente central**: coleta e envia ao Elasticsearch |
| **Elasticsearch** | Mecanismo de busca e análise de código aberto, para grandes volumes | **Indexa e armazena**, com busca e análise |
| **Kibana** | Plataforma de visualização de código aberto, em tempo real | **Visualiza**: painéis, buscas avançadas, relatórios |

**Três abordagens para capturar logs**: direto pela aplicação · agente no nó · Pod auxiliar.

**No Kubernetes**: Elasticsearch como **Service + StatefulSet**, Kibana como **Service NodePort + Deployment**, e Fluentd como **ServiceAccount + ClusterRole + ClusterRoleBinding + DaemonSet**. → [[K8S2 02 - Logs e monitoramento com EFK]]

**No EKS** (aula 9): **Fluentd e Fluent Bit** aparecem como as ferramentas de **logging** suportadas. O Fluentd também pode enviar logs ao **CloudWatch** ([[K8S2 09 - Monitoramento e logging do EKS]]).

> [!tip] Dica do PDF: **não construa seu próprio ecossistema!** Busque componentes já desenvolvidos, que não "reinventem a roda".

## O Elasticsearch na disciplina OpenTelemetry
- **Aula 2**: é uma das opções mais comuns de **storage** do [[Jaeger]], junto com o Cassandra.
- **Aula 4**: é o exemplo de sistema tradicional com **indexação de texto completo**: pesquisas rápidas e flexíveis, mas com custo alto de CPU, memória e disco. É o contraste com o [[Grafana Loki]].

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
No Hands On, o **Elasticsearch** é instanciado para receber os logs, o **Logstash** faz transformações nos logs antes de indexá-los no Elastic e o **Kibana** é usado para explorá-los, com gráficos e dashboard. Aqui a ferramenta de transformação é o **Logstash**, não o Fluentd ([[MS2 06 - Realizando o deploy de microsserviços, parte 2]]).

Aparece em: [[K8S2 02 - Logs e monitoramento com EFK]], [[K8S2 09 - Monitoramento e logging do EKS]], [[OTEL 02 - OpenTelemetry Tracing (Jaeger)]], [[OTEL 04 - OpenTelemetry Logs (Loki)]], [[MS2 06 - Realizando o deploy de microsserviços, parte 2]]
