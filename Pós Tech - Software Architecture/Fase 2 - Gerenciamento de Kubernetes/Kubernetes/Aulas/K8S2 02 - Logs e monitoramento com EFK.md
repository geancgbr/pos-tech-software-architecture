---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 2
fonte: "Kubernetes parte 2/Aula 2.pdf (Thiago Adriano)"
---

# K8S2 02 - Logs e monitoramento com EFK

← [[K8S2 01 - Jobs e CronJobs]] · [[Kubernetes]] · Próxima → [[K8S2 03 - Helm]]

> [!summary] Em uma frase
> O mecanismo nativo de logs do Kubernetes **não é suficiente**, porque os logs precisam de um **ciclo de vida independente** dos Pods e contêineres. O **[[EFK (Elasticsearch, Fluentd e Kibana)|EFK]]** resolve: o **Fluentd** coleta, o **Elasticsearch** indexa e armazena, e o **Kibana** visualiza.

## Hands On
Exemplos práticos de coleta e visualização de logs num ambiente Kubernetes com Elasticsearch, Fluentd e Kibana, e os conceitos básicos de cada componente.

## Logs e monitoramento
- **Monitoramento e observabilidade** permitem entender o que está acontecendo com o sistema, verificar **saúde e erros** e, em estágios mais maduros, **extrair indicadores de negócio**.
- **Gravação de logs**: a maioria das aplicações, serviços e servidores grava, num sistema de IO, registros e eventos sobre o comportamento e a saúde dos componentes.
- **Por que o nativo não basta**: é preciso acessar registros de contêineres e Pods **finalizados por erro ou até excluídos**.

**Três abordagens para capturar logs**
1. **Direto pela aplicação**: ela envia os logs a um serviço de armazenamento perene.
2. **Agente instalado no nó**: coleta os registros e os envia a um repositório.
3. **Pod auxiliar**: coleta os registros e os envia a um serviço ou API de terceiros.

> [!tip] Dica do PDF
> **Não construa seu próprio ecossistema!** Busque componentes já desenvolvidos, que não "reinventem a roda". Em observabilidade, não vale a pena desenvolver a solução inteira.

## EFK
| Componente | O que é | Papel no EFK |
|---|---|---|
| **Elasticsearch** | Mecanismo de **busca e análise** de dados, código aberto, para grandes volumes | **Indexa** os logs recebidos do Fluentd e fornece **busca e análise** |
| **Fluentd** | **Coletor de logs** de código aberto (arquivos, stdout, syslog) | O **componente central**: coleta de várias fontes e **envia ao Elasticsearch** |
| **Kibana** | Plataforma de **visualização** de dados em tempo real, código aberto | **Visualiza** o que o Elasticsearch indexou: painéis, buscas avançadas e relatórios em tempo real |

## Configurando o EFK no Kubernetes
**1. Elasticsearch**: um **Service** (que serve como um "DNS" para o Elastic) e um **StatefulSet** (estrutura de **armazenamento de dados perenes**).
- **Service** `elasticsearch`: `clusterIP: None`, portas **9200** (`rest`) e **9300** (`inter-node`). Criar com `kubectl apply -f (arquivo).yaml` e conferir com **`kubectl get svc`**.
- **StatefulSet** `es-cluster`: `serviceName: elasticsearch`, **1 réplica**, imagem `docker.elastic.co/elasticsearch/elasticsearch:7.2.0`, CPU com limite `1000m` e request `100m`, volume `data` em `/var/lib/elasticsearch/data`, variáveis `cluster.name: k8s-logs`, `discovery.seed_hosts`, `cluster.initial_master_nodes` e `ES_JAVA_OPTS: "-Xms512m -Xmx512m"`.
  - **initContainers** (busybox, `privileged: true`): `fix-permissions` (`chown -R 1000:1000` no diretório de dados), `increase-vm-max-map` (`sysctl -w vm.max_map_count=262144`) e `increase-fd-ulimit` (`ulimit -n 65536`).
  - **volumeClaimTemplates**: `accessModes: ["ReadWriteOnce"]`, **3Gi** de armazenamento.
- **Erro como `ImagePullBackOff`**: remover com `kubectl delete statefulsets es-cluster`, esperar o volume e o Pod saírem, baixar a imagem com `docker pull docker.elastic.co/elasticsearch/elasticsearch:8.3.2` e aplicar de novo.

> [!note] O YAML do StatefulSet usa a imagem `elasticsearch:7.2.0`, mas o `docker pull` sugerido no erro baixa a `8.3.2`. Está assim no PDF.

**2. Kibana**: um **Service** (o "DNS" do Kibana) e um **Deployment**.
- **Service** `kibana-np`: `type: NodePort`, `port: 8080`, `targetPort: 5601`, `nodePort: 30000`.
- **Deployment** `kibana`: 1 réplica, imagem `docker.elastic.co/kibana/kibana:7.5.0`, `ELASTICSEARCH_URL: http://elasticsearch:9200`, `containerPort: 5601`.
- `kubectl apply -f .\(arquivo)-service.yaml` e `kubectl apply -f .\(arquivo)-deployment.yaml`.

**3. Fluentd**: num **único YAML**, os quatro requisitos:

| Recurso | Papel |
|---|---|
| **ServiceAccount** `fluentd` | O texto chama de "um service" (ver nota abaixo) |
| **ClusterRole** `fluentd` | Regra de cluster para **ter acesso aos logs**: `get`, `list` e `watch` sobre `pods` e `namespaces` |
| **ClusterRoleBinding** `fluentd` | Liga a ClusterRole à ServiceAccount (namespace `default`). O PDF diz que é "responsável por monitorar e capturar os eventos de fato do nosso cluster baseado na regra determinada na clusterRole" |
| **DaemonSet** `fluentd` | **Captura os dados no nível de nó** dos Pods. Imagem `fluent/fluentd-kubernetes-daemonset:v1.4.2-debian-elasticsearch-1.1`, apontando para `elasticsearch.default.svc.cluster.local:9200` (`http`), com `hostPath` em `/var/log` e `/var/lib/docker/containers` (somente leitura) |

> [!note] O texto lista "um service" entre os quatro requisitos do Fluentd, mas o YAML define um `ServiceAccount`.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
