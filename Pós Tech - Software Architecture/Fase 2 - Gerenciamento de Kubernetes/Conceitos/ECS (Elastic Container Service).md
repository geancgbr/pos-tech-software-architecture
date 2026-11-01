---
tags: [pos-tech/fase-2, docker, conceito, aws]
aliases: [ECS, Elastic Container Service, Amazon ECS, Fargate, Definição de tarefa, Task Definition]
---

# ECS (Elastic Container Service)

Serviço de **gerenciamento de contêineres da AWS**: executa, escala e gerencia **contêineres Docker num cluster de servidores**.

| Conceito | O que é |
|---|---|
| **Cluster** | Conjunto lógico de **instâncias EC2 ou tarefas Fargate**, onde os contêineres rodam |
| **Tarefa** | A **menor unidade de execução**, descrita por uma **definição de tarefa** (imagem, CPU, memória, portas, variáveis de ambiente) |
| **Serviço** | Mantém **N tarefas** rodando, reinicia as que falham e pode balancear a carga |

**EC2 × Fargate**: EC2 dá **mais controle** sobre as instâncias; Fargate é **serverless**, sem servidores para gerenciar.

**Integrações**: **IAM** (acesso) · **CloudWatch** (monitoramento) · **ELB** (balanceamento). **Segurança**: políticas de IAM e **VPCs** para isolar recursos. **Auto-scaling** por CPU e memória.

**Fluxo de credenciais**: credenciais da instância (metadados do EC2) → credenciais de função (agente do ECS) → tarefa iniciada com o segredo do contêiner → credenciais da tarefa.

**Casos de uso**: desenvolvimento e teste · microsserviços · alto desempenho · Big Data e processamento em lote.

Detalhes: [[DK 06 - ECS]]

## Na disciplina Desenvolvimento Serverless (Fase 3)
- **AWS Fargate**: serverless, com cobrança diferente do Lambda; executa aplicações mais complexas em containers, compatível com **ECS e EKS**, sem cuidar das instâncias ([[SLS 01 - Recursos serverless na AWS]]).
- **Conceitos** ([[SLS 03 - ECS Fargate e ECR]]): computação por **EC2 ou Fargate** · **cluster** · **task definition** (portas, variáveis, memória, CPU, logs) · **task role** (permissões da aplicação) e **task execution role** (logs, acesso ao ECR) · **task** (inclusive rotinas e cron jobs rápidos) · **service** (resiliência, auto scaling e load balancer).
- **Rede** ([[SLS 04 - VPC, Load Balancer e API Gateway]]): cluster e **ALB** numa **subnet privada**, com o **API Gateway** chegando por **VPC Link**.
