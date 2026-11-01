---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 1
fonte: "Kubernetes parte 2/Aula 1.pdf (Thiago Adriano)"
---

# K8S2 01 - Jobs e CronJobs

← [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]] · [[Kubernetes]] · Próxima → [[K8S2 02 - Logs e monitoramento com EFK]]

> [!summary] Em uma frase
> Até aqui, as aplicações eram **reativas** (iniciadas por um estímulo externo). Aplicações de **batch** são "acordadas" num período ou frequência. Para elas, o Kubernetes tem o **Job** (executa uma vez, sob demanda, e seus Pods são removidos ao final) e o **CronJob** (periodicidade configurada na tag **`schedule`**). Ver [[Jobs e CronJobs]].

## Hands On
Como trabalhar com Jobs e CronJobs para automatizar a execução de tarefas em contêineres, com tarefas rotineiras como **criar um backup** ou **disparar uma rotina para limpar um disco**.
- **Jobs**: trabalhos de **curta duração**, executados **apenas uma vez ou um número limitado de vezes**.
- **CronJobs**: **agendam** a execução de tarefas em **horários específicos**.

## Jobs
- Executam trabalhos em contêineres que precisam rodar **apenas uma vez ou num horário agendado**: processamento de dados, geração de relatórios, backups.
- São um **objeto do Kubernetes** com a especificação do trabalho: a **imagem** do contêiner, os **parâmetros de entrada**, a **quantidade de réplicas** etc.
- Ao criar um Job, o Kubernetes cria um **conjunto de Pods**, e cada Pod executa **uma instância do trabalho**, conforme a quantidade de réplicas.
- **A grande diferença**: quando o Job **termina**, o Kubernetes **remove automaticamente os Pods** criados para ele. Os Pods vistos até agora **continuam UP até uma interação nossa**. Se o Job for agendado, o Kubernetes cria um **novo conjunto de Pods** a cada execução.

**YAML de exemplo**
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: fiap-job
spec:
  ttlSecondsAfterFinished: 100
  template:
    spec:
      containers:
      - name: hello
        image: busybox:1.28
        command:
        - /bin/sh
        - -c
        - date; echo Ola Fiap curso de Kubernetes
      restartPolicy: Never
```
> [!note] A indentação do YAML foi refeita, porque a extração do PDF perdeu os recuos.


| Campo | Significado |
|---|---|
| `apiVersion` | Versão da API usada para criar o Job: **`batch/v1`** |
| `kind` | O tipo de objeto: **Job** |
| `metadata` | Informações adicionais, como o nome (**"fiap-job"**) |
| `spec` | A especificação do Job, incluindo a do Pod |
| `ttlSecondsAfterFinished` | Tempo, em segundos, que o Job é **mantido após a conclusão**. Depois disso, o Kubernetes **remove o Job** (aqui, **100 s**) |
| `template` | A especificação do Pod criado pelo Job |
| `containers` / `name` / `image` | Um contêiner **"hello"**, imagem **busybox:1.28** |
| `command` | Exibe a data e a mensagem "Ola Fiap curso de Kubernetes" |
| `restartPolicy` | **`Never`**: o Pod **não é reiniciado em caso de falha** |

**Executando**
```bash
kubectl apply -f .\jobs.yaml    # → job.batch/fiap-job created
kubectl get pods                # verifica a execução (Figura 1)
kubectl get pods                # depois do tempo, confirma que o Job foi deletado (Figura 2)
```

> [!note] O PDF diz que os Jobs rodam "apenas uma vez ou em um horário agendado", e que um Job agendado ganha novos Pods a cada execução. Mais adiante, diz que "o Job executa uma única vez e trabalha sob demanda", e que a periodicidade vem do CronJob.

## CronJobs
- O Job executa **uma única vez**, sob demanda. O **CronJob** permite configurar a **periodicidade** pela tag **`schedule`** (Figura 3).
- Exemplos do PDF: **"00\*\*\*"** para rodar **diariamente à meia-noite**; **"0\*\*\*\*"** para uma tarefa diária **a partir da primeira hora do dia** (grafados assim, sem espaços, no texto extraído).
- Os asteriscos são **posicionais**, da esquerda para a direita, conforme a tabela da **Figura 4 do PDF**.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
