---
tags: [pos-tech/fase-3, serverless, indice]
disciplina: Desenvolvimento Serverless
fase: 3
aulas: 6
---

# Desenvolvimento Serverless

[[Fase 3 - Monitoramento]] · Revisão → [[Revisão - Desenvolvimento Serverless]]

Autor dos PDFs: **Luiz Zenha**.

> [!note] Os PDFs não indicam a fase nem trazem título por aula. A disciplina ficou na Fase 3 porque chegou junto com as outras desta fase; os nomes das notas descrevem o conteúdo.

## O cenário que atravessa as aulas
Uma empresa fictícia de **venda de ingressos on-line**, com data center **on-premises**, migra para a **AWS** usando **[[Serverless|serverless]]** ao máximo, para reduzir custos e aguentar os picos de venda de novos lotes de shows.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[SLS 01 - Recursos serverless na AWS]] | [[Serverless]], [[AWS Lambda]], Fargate, SQS/SNS, [[Amazon DynamoDB]] |
| 2 | [[SLS 02 - Custos serverless na AWS]] | Custos do Lambda, do API Gateway e do DynamoDB; AWS Pricing Calculator |
| 3 | [[SLS 03 - ECS Fargate e ECR]] | [[ECS (Elastic Container Service)\|ECS Fargate]], [[Repositórios de Imagens Docker\|ECR]] |
| 4 | [[SLS 04 - VPC, Load Balancer e API Gateway]] | VPC, ALB × NLB, target groups, HTTP/REST/WebSocket API, VPC Link |
| 5 | [[SLS 05 - Amazon Cognito e OAuth 2.0]] | [[Amazon Cognito]], OAuth 2.0 |
| 6 | [[SLS 06 - AWS Lambda e AWS SAM]] | [[AWS Lambda]], [[AWS SAM]] |

## A arquitetura que vai se montando
| Aula | O que a empresa faz |
|---|---|
| 2 | POC: API Gateway → Lambda → DynamoDB, com estimativa de ~17,98 USD/mês |
| 3 | Teste com a API em container no **ECS Fargate**, imagem no **ECR** |
| 4 | **ALB** e ECS numa **subnet privada**, com o **API Gateway** por **VPC Link** |
| 5 | **Cognito** autenticando as chamadas ao API Gateway com **JWT** |
| 6 | API com **Lambda**, criada e implantada com o **SAM** |

A tabela é só um mapa de navegação, montado a partir das aulas.

## Ligações com outras disciplinas
- **Dockerização (Fase 2)**: o [[ECS (Elastic Container Service)|ECS]] e o [[Repositórios de Imagens Docker|ECR]] também aparecem na Fase 2; aqui o ECS roda com **Fargate** e a imagem vai para o ECR (repositório e login pelo AWS CLI; `docker tag` e `docker push`).
- **API Gateway (Fase 3)**: o **Amazon API Gateway** é a porta de entrada das APIs da empresa ([[API Gateway]]).
- **Arquitetura de Software (Fase 1)**: a aula 2 é uma **POC** ([[Spike e POC]]).

## Material
PDFs em `~/Desktop/Desenvolvimento Serverless/` ("Desenvolvimento Serverless - Aula 1.pdf" a "Aula 6.pdf").
