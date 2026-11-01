---
tags: [pos-tech/fase-2, kubernetes, revisao]
disciplina: Kubernetes
---

# Revisão - Kubernetes

[[Kubernetes]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Parte 1 · Aula 1 - Introdução
> [!question]- Quais dois problemas comuns motivam o uso de contêineres, segundo a aula?
> **Gestão de múltiplos ambientes** (dev, testes, produção minimamente parecidos) e **escalabilidade** (crescer ou encolher conforme a demanda, como na Black Friday). → [[K8S1 01 - Introdução ao Kubernetes]]

> [!question]- Diferença entre virtualização e contêiner?
> A VM cria uma máquina completa (hardware e SO) e compartilha só o hardware. O contêiner fica na camada do SO e compartilha hardware **e** SO, sendo muito mais leve e barato. → [[Contêiner]]

> [!question]- Escalabilidade horizontal × vertical?
> Horizontal: criar e destruir recursos computacionais por demanda. Vertical: expandir os recursos físicos (on-premise ou nuvem). → [[Escalabilidade]]

> [!question]- Quais responsabilidades o Kubernetes assume?
> Criar e destruir contêineres a partir de uma imagem e manter a infraestrutura operacional: se um contêiner falha, cabe ao K8S criar outro.

> [!question]- O que é o Minikube, e por que usá-lo?
> Uma implementação leve do Kubernetes que cria uma VM local com um cluster de um nó só, a melhor indicação para estudos e desenvolvimento local. Precisa de um mecanismo de virtualização (o Docker). → [[Minikube]]

> [!question]- Quais três ferramentas preparam o ambiente, e como validar cada uma?
> kubectl (`kubectl version --output=yaml`), Docker (`docker -v`) e Minikube (`minikube start`, depois `kubectl get pods`).

## Parte 1 · Aula 2 - kubectl e API
> [!question]- O que é o kubectl e como ele se conecta ao cluster?
> O CLI para interagir com o cluster. Roda localmente e faz solicitações RESTful à API do Kubernetes, usando o **kubeconfig** (endereço da API, credenciais e contexto). → [[kubectl]]

> [!question]- Quais os três comandos principais citados?
> `get` (saúde e configurações), `create` (criação) e `delete` (remoção).

> [!question]- Como criar, listar e remover um pod nginx?
> `kubectl run nginx --image=nginx:1.14.2 --port:80` (assim no PDF), `kubectl get pods` e `kubectl delete pod nginx`. → [[K8S1 02 - kubectl e a API do Kubernetes]]

> [!question]- Como a API do Kubernetes é organizada?
> É RESTful (GET, POST, PUT, DELETE), extensível e dividida em grupos. O grupo **core** tem os recursos fundamentais (pods, serviços, replicaset).

## Parte 1 · Aula 3 - Pods, rótulos e anotações
> [!question]- Quais são os componentes de um cluster e o papel de cada um?
> Master node (gerencia e decide onde e como rodar os Pods), worker node (executa os Pods), etcd (banco distribuído com o estado), kubelet (agente em cada node) e kube-proxy (encaminha o tráfego). → [[Cluster Kubernetes]]

> [!question]- O que é um Pod?
> A abstração de um único processo em execução: um ou mais contêineres que compartilham rede e armazenamento. É efêmero, criado por YAML ou JSON, e recebe um IP interno. → [[Pod]]

> [!question]- Rótulos × anotações?
> Ambos são chave-valor. Os rótulos identificam e **selecionam** objetos (ex.: `app: myapp`). As anotações são metadados **não usados em seleção** (ex.: `author: Thiago S Adriano`).

## Parte 1 · Aula 4 - Services e ConfigMap
> [!question]- Quais os três tipos de Service, e qual é o padrão?
> **ClusterIP** (padrão, só dentro do cluster), **NodePort** (porta do nó, acesso externo) e **LoadBalancer** (balanceador externo, IP externo). → [[Service do Kubernetes]]

> [!question]- Para que serve o ConfigMap, e como injetá-lo?
> Separa as configurações do contêiner dos artefatos de implantação, num local centralizado. Injeção por variáveis de ambiente, arquivos montados ou argumentos de linha de comando (no exemplo, `envFrom`). → [[ConfigMap]]

## Parte 1 · Aula 5 - ReplicaSets e Deployments
> [!question]- O que o ReplicaSet garante?
> Que um número específico de réplicas de um conjunto de Pods esteja em execução a qualquer momento. Se uma falha, inicia outra. Seleciona os Pods por seletor de rótulo. → [[ReplicaSet e Deployment]]

> [!question]- Que recursos o Deployment oferece?
> Rolling Update (substituição gradual sem interromper o serviço), rollback (voltar à versão anterior) e dimensionamento horizontal.

> [!question]- Por que se usa mais o Deployment no dia a dia?
> Os arquivos têm pouca diferença, mas o Deployment tem **controle de versão**.

## Parte 1 · Aula 6 - Volumes
> [!question]- Quais os quatro conceitos de armazenamento do Kubernetes?
> Volumes (VOL), persistent volumes (PV), persistent volume claims (PVC) e storage classes (SC). → [[Volumes, PV, PVC e StorageClass]]

> [!question]- emptyDir × hostPath × persistentVolumeClaim?
> emptyDir: vazio, criado e excluído com o Pod, para arquivos temporários entre contêineres. hostPath: monta um diretório ou arquivo do nó. persistentVolumeClaim: armazenamento persistente que sobrevive a reinicializações.

> [!question]- Quais os tipos de PVC?
> ReadWriteOnce (um nó, leitura e gravação), ReadOnlyMany (vários nós, leitura) e ReadWriteMany (vários nós, leitura e gravação).

> [!question]- Cite tipos de PV e de StorageClass.
> PV: NFS, iSCSI, hostPath, EBS. SC: Standard, SSD e SAN.

## Parte 1 · Aula 7 - Probes
> [!question]- Quais as três probes, e o que acontece quando cada uma falha?
> Liveness (está em execução? reinicia o Pod), Readiness (está pronto para solicitações? remove do balanceador de carga) e Startup (está iniciando corretamente? reinicia o Pod). → [[Probes do Kubernetes]]

> [!question]- Como as probes verificam por padrão?
> Por um endpoint HTTP: um GET esperando 200 OK. A Liveness também pode ser TCP ou Exec.

> [!question]- Por que a Readiness é necessária se já existe a Liveness?
> Mesmo em execução, o aplicativo pode ainda não estar pronto (carregando dados ou abrindo conexão com o banco).

> [!question]- Cite boas práticas de probes.
> Usar as três, ajustar os intervalos, endpoints diferentes por probe, preferir as configurações padrão, testar, monitorar com Prometheus, documentar e monitorar as falhas.

> [!question]- Quais os valores do exemplo da aula?
> Liveness a cada 10 s, espera de 5 s. Readiness a cada 5 s, espera de 3 s. Startup com atraso inicial de 120 s, a cada 30 s, espera de 10 s.

## Parte 1 · Aula 8 - HPA
> [!question]- Como o HPA funciona?
> Monitora métricas de utilização (CPU, memória...) e compara com limites predefinidos: quando a utilização ultrapassa, aumenta as réplicas; quando diminui, diminui. Tem mínimo e máximo de réplicas. → [[HPA (Horizontal Pod Autoscaler)]]

> [!question]- Quais métricas o HPA suporta?
> CPU (a mais comum), memória, métricas personalizadas, medidas externas (como o Prometheus) e E/S de disco.

> [!question]- Como testar o HPA do exemplo?
> O Deployment nginx tem 1 réplica e o HPA vai de 1 a 10, com alvo de 70% de CPU. Gerar carga com o K6 ou o JMeter, conferir com `kubectl get hpa`, reduzir a carga e conferir de novo.

## Parte 2 · Aula 1 - Jobs e CronJobs
> [!question]- Job × CronJob?
> Job: executa uma vez (ou um número limitado de vezes), sob demanda. CronJob: periodicidade configurada na tag `schedule`. → [[Jobs e CronJobs]]

> [!question]- O que acontece com os Pods de um Job ao final?
> São removidos automaticamente. Os Pods comuns continuam UP até uma interação nossa.

> [!question]- O que significam `ttlSecondsAfterFinished: 100` e `restartPolicy: Never`?
> O Job é removido 100 s depois de concluído; o Pod não é reiniciado em caso de falha.

## Parte 2 · Aula 2 - EFK
> [!question]- Por que o mecanismo nativo de logs do Kubernetes não basta?
> Os logs precisam de um ciclo de vida independente dos Pods e contêineres, para acessar registros de Pods finalizados por erro ou excluídos. → [[K8S2 02 - Logs e monitoramento com EFK]]

> [!question]- Quais as três abordagens para capturar logs?
> Direto pela aplicação, um agente instalado no nó ou um Pod auxiliar.

> [!question]- Qual o papel de cada letra do EFK?
> Fluentd coleta (o componente central) e envia ao Elasticsearch, que indexa, armazena e permite buscar. O Kibana visualiza. → [[EFK (Elasticsearch, Fluentd e Kibana)]]

> [!question]- Como cada componente é criado no Kubernetes?
> Elasticsearch: Service + StatefulSet. Kibana: Service NodePort + Deployment. Fluentd: ServiceAccount + ClusterRole + ClusterRoleBinding + DaemonSet.

> [!question]- Qual a dica do PDF sobre ferramentas de observabilidade?
> Não construa seu próprio ecossistema: use componentes prontos, sem reinventar a roda.

## Parte 2 · Aula 3 - Helm
> [!question]- O que é o Helm, e o que é um chart?
> Um gerenciador de pacotes para o Kubernetes. O chart é o pacote com todos os recursos para implantar um aplicativo, com nome e versão, guardado num repositório. → [[Helm]]

> [!question]- O que há em `Chart.yaml` e em `values.yaml`?
> Chart.yaml: nome, versão e descrição. values.yaml: os valores padrão das configurações.

> [!question]- Quais comandos criam e empacotam um chart?
> `helm create primeiro-chart` e `helm package` (gera um `.tgz`).

## Parte 2 · Aula 4 - EKS
> [!question]- Por que usar Kubernetes na nuvem?
> No próprio ambiente é preciso provisionar servidores e assumir instalação e gestão. Na nuvem: sem provisionamento de hardware e sem custo de gestão. → [[K8S2 04 - EKS]]

> [!question]- Como as responsabilidades se dividem no EKS?
> A AWS gerencia a infraestrutura (servidores, rede e armazenamento); você gerencia os aplicativos em contêineres. → [[EKS (Elastic Kubernetes Service)]]

> [!question]- Amazon VPC CNI × Calico?
> VPC CNI: padrão e recomendada, Pods com IPs privados da VPC. Calico: de terceiros, com segurança extra, como separar o tráfego entre namespaces.

> [!question]- O que é o control plane?
> O componente central que gerencia o estado do cluster e coordena os worker nodes. Configuração: versão, segurança, autenticação e autorização.

## Parte 2 · Aulas 5 e 6 - AWS EKS na prática
> [!question]- Quais os passos da migração do IIS para o EKS?
> Avaliar o aplicativo (dependências, requisitos, reunião com infra e dev, desenho), criar a imagem Docker (guardada num registro como o ECR) e criar os objetos do Kubernetes (Deployment, Service e, se necessário, Ingress). → [[K8S2 05 - AWS EKS na prática, parte 1]]

> [!question]- Para que serve o Ingress no exemplo?
> Rotear o tráfego externo: associa `my-nodejs-app.example.com` ao `my-nodejs-app-service` na porta 80.

> [!question]- Por que usar o HPA no EKS?
> Para escalar automaticamente conforme o tráfego, sem intervenção manual. Sem ele, a escala fica nas configurações manuais, com risco de interrupções e erros humanos. → [[K8S2 06 - AWS EKS na prática, parte 2]]

> [!question]- O que é o K6, e o que faz `k6 run --vus 10 --duration 30s test.js`?
> Ferramenta de código aberto para testes de carga em JavaScript (HTTP, WebSocket, gRPC). O comando roda o script com 10 usuários virtuais por 30 segundos.

## Parte 2 · Aula 7 - CI/CD
> [!question]- Como a aula define CI e CD?
> CI: integrar as alterações ao projeto principal com frequência, várias vezes ao dia. CD: implantação (ou entrega) contínua, implantando as alterações de forma automatizada em teste e produção. → [[K8S2 07 - Kubernetes CI-CD]]

> [!question]- Quais ambientes o exemplo de CD tem, e qual ação implanta?
> Desenvolvimento, homologação e produção, cada um com app-name, slot e perfil de publicação próprios, usando o `Azure/webapps-deploy@v2`.

## Parte 2 · Aula 8 - Segurança
> [!question]- IAM × RBAC?
> IAM: identidades da AWS (usuários, grupos, funções) e permissões sobre o EKS. RBAC: permissões granulares por usuário ou grupo, com regras baseadas em namespaces, Pods, serviços etc. → [[RBAC no Kubernetes]]

> [!question]- O que fazem a ClusterRole e o RoleBinding do exemplo?
> A ClusterRole `exemple-role` permite get, watch e list em Pods; o RoleBinding associa essa função ao usuário `tadriano`.

> [!question]- Como verificar se um usuário tem uma permissão?
> `kubectl auth can-i get pods --as tadriano`.

## Parte 2 · Aula 9 - Monitoramento e logging
> [!question]- Quais ferramentas de monitoramento e logging o EKS suporta?
> Amazon CloudWatch, Prometheus (monitoramento) e Fluentd e Fluent Bit (logging). → [[K8S2 09 - Monitoramento e logging do EKS]]

> [!question]- CloudWatch Logs × Logs Insights?
> Logs armazena e pesquisa logs em grupos de logs com streams. Logs Insights faz consultas ad hoc para análise e resolução de problemas. → [[Amazon CloudWatch]]

> [!question]- Como o Prometheus coleta métricas?
> Pelo modelo **pull**: solicita as métricas dos servidores e aplicativos monitorados em intervalos regulares e as guarda num banco de séries temporais. → [[Prometheus]]

> [!question]- Qual o papel do Grafana?
> Visualizar métricas (por exemplo, do Prometheus) em painéis personalizados e criar alertas antes que os problemas se tornem críticos. → [[Grafana]]

## Dúvidas em aberto
- Parte 1, aula 2: o comando aparece como `--port:80` no PDF.
- Parte 1, aula 4: as Figuras 2 a 5 têm a legenda "Criação de um service com ClusterIP", mas o texto descreve um Pod e um ConfigMap.
- Parte 1, aula 5: o PDF diz que os ReplicaSets são "uma extensão do conceito de Deployment".
- Parte 2, aula 1: o PDF diz que os Jobs rodam "apenas uma vez ou em um horário agendado", mas depois que o Job "executa uma única vez e trabalha sob demanda" e que a periodicidade é do CronJob.
- Parte 2, aula 2: o StatefulSet usa a imagem `elasticsearch:7.2.0`, mas o `docker pull` sugerido baixa a `8.3.2`. O texto também chama de "service" o que o YAML define como `ServiceAccount`.
- Parte 2, aula 4: o texto diz "por mais que a escalabilidade promovida pela solução seja vertical".
- Parte 2, aula 7: o texto fala em Azure DevOps, mas os YAML usam elementos de GitHub Actions.
- Parte 2, aula 8: os nomes variam entre "exemple" e "example", e o texto diz que o usuário pode "acessar e modificar" Pods com uma role que só tem get, watch e list.
- Parte 2, aula 9: o PDF diz que o EFK foi visto "na aula anterior", mas ele foi tratado na aula 2.

## Pontos fracos (o que errei)
