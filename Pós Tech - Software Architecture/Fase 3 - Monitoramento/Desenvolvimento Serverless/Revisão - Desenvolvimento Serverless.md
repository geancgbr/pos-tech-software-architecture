---
tags: [pos-tech/fase-3, serverless, revisao]
disciplina: Desenvolvimento Serverless
---

# Revisão - Desenvolvimento Serverless

[[Desenvolvimento Serverless]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Recursos serverless
> [!question]- O que é serverless?
> Uma arquitetura nativa da nuvem que transfere boa parte das responsabilidades operacionais e de infraestrutura para o provedor cloud. → [[Serverless]]

> [!question]- Lambda × Fargate: quando usar cada um no cenário?
> Lambda: rotinas, scripts rápidos e APIs menores, para não deixar recurso rodando sem uso. Fargate (ECS): microsserviços de execução contínua, com processamento e memória mais intensos.

> [!question]- SQS × SNS?
> SQS: fila de mensagens processadas conforme chegam, evitando timeouts e sobrecarga. SNS: notificações por tópicos, entregues de uma vez a todos os assinantes (SMS, e-mail, HTTPS, SQS).

> [!question]- Para que servem o EventBridge, o Step Functions e o AppSync?
> EventBridge: aplicações e serviços publicam e têm respostas de eventos em tempo real. Step Functions: orquestrar fluxos de trabalho com editor visual. AppSync: back-end com dados em tempo real via GraphQL.

> [!question]- EFS × S3?
> EFS: sistema de arquivos acessado por vários sistemas. S3: armazenamento de objetos, acessado por API REST ou SDKs.

> [!question]- O que são o RDS Proxy e o Redshift Serverless, segundo a aula?
> O RDS Proxy não é banco de dados: gerencia as conexões com bancos RDS. O Redshift Serverless não é diretamente um banco: faz análises em tempo real.

## Aula 2 - Custos
> [!question]- Por que a POC precisa de API Gateway?
> Porque, por si só, o Lambda não expõe uma API RESTful. → [[SLS 02 - Custos serverless na AWS]]

> [!question]- Como o Lambda é cobrado?
> Por solicitações e por duração (arredondada para 1 ms), com preço base que sobe com a memória; free tier de 1 milhão de solicitações e 400.000 GB-s por mês; x86 e ARM têm tabelas diferentes. → [[AWS Lambda]]

> [!question]- API Gateway REST × HTTP?
> REST: mais completo (chaves de API, limitação por cliente, validação, AWS WAF, endpoints privados) e mais caro. HTTP: mais simples e mais barato.

> [!question]- DynamoDB on-demand × provisioned?
> On-demand: paga pelo uso, bom para ambientes imprevisíveis. Provisioned: especifica leituras e escritas, com desempenho garantido e previsibilidade financeira. → [[Amazon DynamoDB]]

> [!question]- Qual foi a estimativa da POC?
> Cerca de 17,98 USD por mês (215,76 USD por ano), sem considerar o free tier.

## Aula 3 - ECS Fargate e ECR
> [!question]- Quais os benefícios do ECS Fargate?
> Simplificação da infraestrutura, escalabilidade automática, containers só quando necessário e execução isolada e segura. → [[SLS 03 - ECS Fargate e ECR]]

> [!question]- Task role × task execution role?
> Task role: as permissões que a aplicação precisa na AWS (ex.: S3, Secrets Manager). Task execution role: o que o container terá, como coleta de logs e acesso ao ECR.

> [!question]- Task × service no ECS?
> A task executa a aplicação; o service garante que as tasks rodem de forma resiliente e escalável, com auto scaling e load balancer.

> [!question]- Quais comandos publicam a imagem no ECR?
> `aws ecr create-repository`, `aws ecr get-login-password | docker login`, `docker tag` e `docker push`.

## Aula 4 - VPC, Load Balancer e API Gateway
> [!question]- Por que deixar a API numa subnet privada?
> Porque um banco exposto publicamente pode ser um risco de invasão gravíssimo, e uma API sem segurança nas rotas numa subnet pública poderia ter o IP descoberto e ser atacada. → [[SLS 04 - VPC, Load Balancer e API Gateway]]

> [!question]- Internet Gateway × NAT Gateway?
> Internet Gateway: a porta de entrada para a internet pública. NAT Gateway: permite que recursos de uma sub-rede privada acessem a internet.

> [!question]- ALB × NLB?
> ALB: o mais moderno, com gRPC, roteamento por requisição, respostas estáticas e redirecionamentos; um pouco mais caro. NLB: trabalha com TCP, UDP e TLS.

> [!question]- Para que servem os target groups?
> Identificar os alvos e verificar a saúde deles por health checks (ex.: um endpoint que devolve 200 ou 500), ajudando o ECS a substituir tasks não saudáveis.

> [!question]- HTTP API × REST API × WebSocket API?
> HTTP: mais nova, leve e barata, para casos simples. REST: mais antiga e completa, para casos complexos. WebSocket: comunicação bidirecional em tempo real.

> [!question]- O que é o VPC Link?
> Um recurso do API Gateway para integrar com segurança APIs privadas numa VPC (um NLB ou uma VPC). Tem taxas adicionais.

## Aula 5 - Cognito e OAuth
> [!question]- O que é o OAuth 2.0?
> Um protocolo padrão da indústria para autorização, que dá acesso a recursos sem expor as credenciais, como uma chave temporária. → [[Amazon Cognito]]

> [!question]- Quais os três fluxos do OAuth citados?
> Authorization Code Grant (código trocado pelo token), Implicit Grant (token exposto ao usuário; só se o primeiro não der) e Client Credentials Grant (M2M, com ID e Secret).

> [!question]- User pools × identity pools?
> User pools: diretório para autenticar e autorizar no app ou na API, emitindo JWTs. Identity pools: emitem credenciais da AWS para usuários autenticados ou anônimos acessarem recursos da AWS.

## Aula 6 - Lambda e SAM
> [!question]- Como funciona o Lambda?
> Um trigger invoca a função; ao terminar, ela pode ter um destino em caso de sucesso, ou, na falha, por exemplo, iniciar uma função paliativa ou pôr uma mensagem numa fila. → [[AWS Lambda]]

> [!question]- Cite triggers do Lambda.
> API Gateway, AWS IoT, S3 e SNS/SQS.

> [!question]- O que é o AWS SAM, e qual a desvantagem dele?
> Um framework open source para desenvolver, testar e implantar aplicativos serverless, com YAML do CloudFormation e teste local. A desvantagem: o acoplamento com a AWS, que pode restringir a portabilidade. → [[AWS SAM]]

> [!question]- Quais os pré-requisitos do SAM CLI?
> O AWS CLI configurado (credenciais) e o Docker.

## Dúvidas em aberto
- Aula 1: o banco de grafos aparece como "Amazon Neptuno Serverless".
- Aula 5: o OAuth 2.0 aparece como "protocolo de autenticação" e, logo depois, "para autorização".
- Aula 6: o texto chama de primeiro Lambda o criado pelo console; o resumo diz que foi com o SAM CLI.
- Aula 4: o texto escreve "Amazon VPC ou Amazon Private Cloud".

## Pontos fracos (o que errei)
