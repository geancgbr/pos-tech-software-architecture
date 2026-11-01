---
tags: [pos-tech/fase-3, serverless, aws, conceito]
aliases: [Sem servidor, Arquitetura serverless]
---

# Serverless

**Server** (servidor) + **less** (menos): **sem servidor**. Segundo a aula 1, uma **arquitetura nativa da nuvem** que transfere boa parte das responsabilidades **operacionais e de infraestrutura** para o provedor cloud ([[SLS 01 - Recursos serverless na AWS]]).

- Criar e executar aplicativos **sem se preocupar com servidores**: sem provisionar instância ou cluster, configurar e atualizar o SO, cuidar de disco ou processamento.
- Serve para **qualquer tipo de aplicativo ou back-end**; a alta disponibilidade fica com a cloud.
- **No cenário da disciplina**: usar serverless ao máximo para reduzir custos **nas horas em que a plataforma não é usada**.

| Área | Recursos serverless da AWS citados |
|---|---|
| Computação | [[AWS Lambda]], AWS Fargate ([[ECS (Elastic Container Service)\|ECS]] e EKS) |
| Integrações | EventBridge, Step Functions, SQS, SNS, AppSync, Amazon API Gateway |
| Armazenamento | EFS, S3, [[Amazon DynamoDB]], Aurora Serverless, Neptuno Serverless (assim no PDF), RDS Proxy, Redshift Serverless |
| Ferramentas | [[AWS SAM]] |

- O [[Amazon Cognito]] aparece como "não exatamente serverless", mas como serviço que faz a identificação e autorização dos usuários ([[SLS 05 - Amazon Cognito e OAuth 2.0]]).

Aparece em: [[SLS 01 - Recursos serverless na AWS]] a [[SLS 06 - AWS Lambda e AWS SAM]]
