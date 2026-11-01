---
tags: [pos-tech/fase-3, serverless, aws, aula]
disciplina: Desenvolvimento Serverless
aula: 1
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 1.pdf (Luiz Zenha)"
---

# SLS 01 - Recursos serverless na AWS

[[Desenvolvimento Serverless]] · Próxima → [[SLS 02 - Custos serverless na AWS]]

> [!summary] Em uma frase
> **[[Serverless]]** ("sem servidor") é uma **arquitetura nativa da nuvem** que transfere boa parte das responsabilidades **operacionais e de infraestrutura** para o provedor cloud (aqui, a **AWS**). A aula percorre os recursos serverless da AWS para **computação** (Lambda, Fargate), **integrações** (EventBridge, Step Functions, SQS, SNS, AppSync, API Gateway) e **armazenamento** (EFS, S3, DynamoDB, Aurora Serverless e outros).

> [!note] Os PDFs desta disciplina não trazem título por aula; os nomes das notas descrevem o conteúdo.

## O cenário
Uma empresa fictícia de **venda de ingressos on-line**, com **data center on-premises**. A nova diretoria quer modernizar, com **redução de custos** e otimização, principalmente nos momentos de **alta demanda por novos lotes de shows**, que geram reclamações. O plano é migrar para a **cloud** usando **serverless ao máximo**, sobretudo para reduzir custos **nas horas em que a plataforma não é usada**.

## Hands On
Os recursos serverless da AWS, de **APIs com o AWS Lambda** a **banco de dados com o AWS RDS** e **tópicos e filas com SQS e SNS**, e **em que momento** é adequado usar um serviço serverless.

> [!note] O Hands On e as palavras-chave citam "banco de dados com os AWS RDS", mas o texto não traz o RDS como banco serverless; só o **RDS Proxy**, que "não é um banco de dados".

## O que é serverless
- **Server** (servidor) + **less** (menos): **sem servidor**.
- Uma **arquitetura nativa da nuvem** que transfere boa parte das responsabilidades operacionais e de infraestrutura ao provedor.
- Criar e executar aplicativos **sem se preocupar com servidores**: sem provisionar instância ou cluster, configurar e atualizar o SO, cuidar de espaço em disco ou capacidade de processamento.
- Serve para **qualquer tipo de aplicativo ou back-end**, e a configuração para rodar com **alta disponibilidade** fica com a cloud.

## Computação
| Serviço | O que o PDF diz | Quando usar (no cenário) |
|---|---|---|
| **[[AWS Lambda]]** | Serviço serverless **orientado a eventos** para executar código de praticamente qualquer aplicação ou back-end. Pode ser chamado a partir de **mais de 200 serviços AWS**, e você **paga só pelo que usar** | **Rotinas, scripts de execução rápida ou APIs menores**, para não deixar um recurso rodando sem uso |
| **AWS Fargate** | Serverless, mas com **cobrança diferente** do Lambda. Executa aplicações **mais complexas em containers** sem cuidar da infraestrutura. Compatível com **ECS** e **EKS**; você não se preocupa com as instâncias que orquestram os containers (como os nós de um cluster Kubernetes) | **Microsserviços** ou aplicações de **execução contínua**, com processamento e memória **mais intensos**, em containers **ECS com Fargate** |

## Integrações
| Serviço | O que o PDF diz |
|---|---|
| **Amazon EventBridge** | Aplicações e serviços **publiquem e tenham respostas de eventos em tempo real**. Ex.: integrar **alertas** de vários sistemas da AWS, com filtros e regras, num sistema que os consolide. Outros usos: plataformas **SaaS**, monitoramento de recursos e integração **on-premises + cloud** (arquitetura **híbrida**). Permitiria uma migração **parcial**, sem mudança brusca |
| **AWS Step Functions** | **Orquestrar fluxos de trabalho**, ordenando e coordenando tarefas, integrado a Lambdas, SQS e SNS, com um **editor visual** de transições, estados e regras de decisão e ramificação |
| **Amazon SQS e SNS** | Serviços de **mensagens** para integrações **assíncronas**, boas opções contra a **baixa performance na alta demanda**. **SQS** = **fila de mensagens**: as mensagens são enfileiradas e processadas conforme chegam, em vez de requisições síncronas com risco de **timeouts** ou sobrecarga. **SNS** = **notificações**: as aplicações **assinam tópicos**; mensagens por SMS, e-mail, HTTPS e até do SQS; todos os assinantes são notificados **de uma só vez**. Ambos são **totalmente serverless** |
| **AWS AppSync** | Back-end para apps **web ou mobile**, com consulta, subscrição e envio de dados **em tempo real**, **sem montar uma API**, consumindo fontes de dados por **APIs GraphQL**. Destaque: **sincronismo de dados em tempo real**. No cenário: atualizar carrinhos, ingressos e lugares disponíveis |
| **Amazon API Gateway** | **"A grande estrela"** da migração: **criar, publicar, monitorar e proteger APIs** sem se preocupar com hardware. Cuida do recebimento até **centenas de milhares de chamadas simultâneas**, **gerenciamento de tráfego**, **CORS**, **autorização e acesso**, **monitoramento** e **versões**. Integra com **Lambdas, containers ou instâncias**. Ver [[API Gateway]] |

## Armazenamento
| Serviço | O que o PDF diz |
|---|---|
| **Amazon EFS** (Elastic File System) | **Sistema de arquivos** acessado por vários sistemas no mesmo local, sem se preocupar com espaço: altamente **escalável e disponível** |
| **Amazon S3** | Armazena **objetos**; **não é sistema de arquivos** como o EFS, então a integração é por **API REST** ou pelos **SDKs** da AWS |
| **Amazon DynamoDB** | Banco **NoSQL** altamente escalável gerenciado pela AWS. Ver [[Amazon DynamoDB]] |
| **Amazon Aurora Serverless** | Banco **SQL** compatível com **MySQL e PostgreSQL**, totalmente serverless, escalável, disponível e resiliente |
| **Amazon Neptuno Serverless** (assim no PDF) | Banco de dados **de grafos**, de alta performance, sem provisionar infraestrutura |
| **Amazon RDS Proxy** | **Não é banco de dados**: gerencia as **conexões** com bancos RDS, para **alta disponibilidade**, segurança, logs e monitoramento |
| **Amazon Redshift Serverless** | **Não é diretamente um banco**: **análises de dados em tempo real** |

## Referências
Ashish (2020): AWS — Serverless services on AWS · AWS: Sem servidor na AWS
