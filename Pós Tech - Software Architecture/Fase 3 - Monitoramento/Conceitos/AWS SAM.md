---
tags: [pos-tech/fase-3, serverless, aws, conceito]
aliases: [SAM, Serverless Application Model, AWS Serverless Application Model, SAM CLI]
---

# AWS SAM

**Framework open source** e amplamente usado para **desenvolver, testar e implantar** aplicativos serverless na AWS ([[SLS 06 - AWS Lambda e AWS SAM]]).

- **Vantagens**: simplicidade; sintaxe **YAML do CloudFormation**; **exemplos de projetos**; **SAM CLI** para criar, testar e implantar pela linha de comando; integração com o **AWS CodePipeline** (implantação contínua); **teste local**, emulando o ambiente da AWS.
- **Pré-requisitos**: **AWS CLI** configurado (credenciais no AWS IAM Identity Center) e **Docker**.
- **Comando**: `sam` valida a instalação; os modelos trazem as instruções de CloudFormation (Lambdas, APIs, tabelas DynamoDB).
- **Desvantagem**: específico da AWS, **pode restringir a portabilidade** e cria **grande acoplamento**; migrar de provedor exige reconstruções.

Aparece em: [[SLS 06 - AWS Lambda e AWS SAM]]
