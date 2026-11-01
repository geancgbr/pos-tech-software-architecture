---
tags: [pos-tech/fase-3, serverless, aws, aula]
disciplina: Desenvolvimento Serverless
aula: 3
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 3.pdf (Luiz Zenha)"
---

# SLS 03 - ECS Fargate e ECR

← [[SLS 02 - Custos serverless na AWS]] · [[Desenvolvimento Serverless]] · Próxima → [[SLS 04 - VPC, Load Balancer e API Gateway]]

> [!summary] Em uma frase
> A diretoria quis um **"teste duplo"** (assim no PDF), e uma equipe verifica a viabilidade de rodar uma aplicação existente no **ECS com Fargate**. É preciso **conteinerizar** a aplicação, fazer o **build** da imagem e **publicá-la no ECR**. O PDF explica **cluster, task definition (task role e task execution role), task e service** e mostra o código, o Dockerfile e os comandos do AWS CLI até o `docker push`.

> [!warning] Custo
> O PDF avisa: executar o **ECS Fargate na sua conta AWS gera custos**, e quanto mais tempo rodando, maiores os custos.

## Hands On
A partir de uma **imagem pública no ECR**, criar e configurar um **cluster do ECS com Fargate**, uma **task definition** para colocar a API no ar e o **service** com suas tasks, e acessar a API por um **endereço provisionado pela AWS**. Segundo o resumo, a imagem foi enviada à AWS e executada como serviço no ECS Fargate, com a execução da API validada.

## Benefícios do ECS Fargate
Simplifica a execução de containers, eliminando a gestão da infraestrutura. Ver [[ECS (Elastic Container Service)]].
- **Simplificação da infraestrutura**: sem cuidar de hardware, atualizações de SO, drivers e outros softwares.
- **Escalabilidade automática**: o Fargate **pode** orquestrar e dimensionar conforme a demanda, sem interrupções.
- **Containers só quando necessário**: gerenciamento eficiente de recursos financeiros.
- **Isolamento**: tarefas e serviços em ambientes **seguros e isolados**.

**Passos**: gerar a imagem Docker → publicar no **ECR** → configurar o **ECS Fargate** → criar o serviço que executa o container.

## Os conceitos do ECS
| Conceito | O que o PDF diz |
|---|---|
| **Computação** | O ECS pode usar **instâncias EC2** ou a tecnologia serverless **Fargate**. Na aula, Fargate, deixando a AWS gerenciar a infraestrutura |
| **Cluster** | Na orquestração, um **agrupamento de instâncias EC2** (assim no PDF, embora a aula use Fargate) com capacidade para executar vários containers |
| **Task definition** | "Definição de tarefa": **como** executar uma task, que pode ter **um ou mais containers**. Define **portas, variáveis de ambiente, memória, CPU** e a **coleta de logs** |
| **Task role** | As **permissões que a aplicação precisa** na AWS (ex.: acessar um **S3**, ler segredos do **Secrets Manager**) |
| **Task execution role** | O **agente** que orquestra o que o container terá: **coleta de logs**, **permissão para acessar o ECR** e baixar a imagem |
| **Task** | Executa aplicações em container (ex.: a API). Também serve para **rotinas ou cron jobs**, se forem rápidas e com horário definido; para tarefas mais complexas, a AWS tem serviços especializados, que podem ter melhor custo-benefício |
| **Service** | Garante que a task rode de forma **resiliente e escalável**: se uma falhar, o ECS executa outras. Permite **auto scaling** pela quantidade de requisições e um **load balancer** entre as tasks |

## Preparando e publicando no ECR
**`app.js`** (Express, porta 3000), que devolve uma lista de shows em `GET /`:
```javascript
const express = require('express');
const app = express();
const port = 3000;

function gerarListaDeShows() {
  return shows = [
    { nome: 'Show 1', data: '10/06/2023', hora: '20:00', local: 'Teatro Municipal', valor_ingresso: 50.00 },
    { nome: 'Show 2', data: '15/06/2023', hora: '19:30', local: 'Centro de Convenções', valor_ingresso: 80.00 },
    { nome: "Show 3", data: "20/06/2023", hora: "21:00", local: "Ginásio Esportivo", valor_ingresso: 35.00 },
    { nome: "Show 4", data: "25/06/2023", hora: "18:30", local: "Praça Central", valor_ingresso: 20.00 },
    { nome: "Show 5", data: "30/06/2023", hora: "20:30", local: "Auditório Universitário", valor_ingresso: 45.00 }
  ];
}

app.get('/', (req, res) => {
  const listaDeShows = gerarListaDeShows();
  res.json(listaDeShows);
});

app.listen(port, () => {
  console.log(`App listening at http://localhost:${port}`);
});
```

**Dockerfile**:
```dockerfile
FROM alpine:latest
RUN apk update
RUN apk add npm
RUN mkdir /app
WORKDIR /app
COPY app.js app.js
RUN npm install express
ENTRYPOINT [ "node", "app.js" ]
EXPOSE 3000
```

**Comandos** (exigem o **AWS CLI** configurado, com as credenciais):
```bash
docker build . -t events:latest
aws ecr --region us-east-1 create-repository --repository-name events   # devolve o repositoryUri (JSON)
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com   # → "Login Succeeded"
docker tag events:latest <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/events:latest
docker push <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/events:latest
```

> [!note] O ID da conta AWS que aparece no PDF foi substituído por `<ACCOUNT_ID>`.

- No `docker tag`, o 1º parâmetro é a imagem (`tag:versão` ou o **imageId**) e o 2º, a **URL do registry:versão**. Depois do push, a imagem aparece no console (Figura 1).

> [!note] A indentação do código foi refeita, e os objetos de `gerarListaDeShows` foram postos um por linha; os valores são os do PDF. O texto do PDF termina no `docker push`; a criação do cluster, da task definition e do service fica no Hands On.

## Referências
AWS: Conceitos básicos do Amazon ECS · Definição de preço do AWS Lambda · Preço do Amazon DynamoDB · Preço do Amazon API Gateway · Sem servidor na AWS
