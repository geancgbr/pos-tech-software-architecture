---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Job, Jobs, CronJob, CronJobs, Cron Jobs, ttlSecondsAfterFinished]
---

# Jobs e CronJobs

Aplicações de **batch** são "acordadas" num período ou frequência, em vez de reagir a um estímulo externo.

| | Job | CronJob |
|---|---|---|
| Execução | **Uma vez** (ou um número limitado de vezes), **sob demanda** | **Periódica**, configurada na tag **`schedule`** |
| Usos | Processamento de dados, relatórios, backups | Tarefas em horários específicos |

- **Ambos** podem ser usados para tarefas rotineiras, como **criar um backup** ou **disparar uma rotina para limpar um disco**.
- Ao criar um Job, o Kubernetes cria **um conjunto de Pods**, um por instância do trabalho, conforme as réplicas. **Ao final, remove os Pods automaticamente.**
- **Exemplo** (`fiap-job`, `batch/v1`): imagem `busybox:1.28`, exibe a data e "Ola Fiap curso de Kubernetes", **`ttlSecondsAfterFinished: 100`** (o Job é removido 100 s depois de concluído) e **`restartPolicy: Never`** (o Pod não é reiniciado em caso de falha).
- **`schedule`**: asteriscos **posicionais**, da esquerda para a direita, conforme a Figura 4 do PDF. Exemplos do texto: "00\*\*\*" (diariamente à meia-noite) e "0\*\*\*\*" (diariamente a partir da primeira hora do dia).

Aparece em: [[K8S2 01 - Jobs e CronJobs]]
