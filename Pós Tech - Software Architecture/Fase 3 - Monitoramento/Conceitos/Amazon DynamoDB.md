---
tags: [pos-tech/fase-3, serverless, aws, conceito]
aliases: [DynamoDB, DynamoDB Streams]
---

# Amazon DynamoDB

Banco de dados **NoSQL altamente escalável**, **gerenciado pela AWS** ([[SLS 01 - Recursos serverless na AWS]]).

- Oferece **segurança integrada, backups, replicação multirregional, cache em memória** e importação e exportação ([[SLS 02 - Custos serverless na AWS]]).

| Modo de cobrança | Como funciona | Vantagem |
|---|---|---|
| **On-demand capacity** | Paga pelo uso | Ambientes ainda imprevisíveis |
| **Provisioned capacity** | Especifica as leituras e escritas esperadas | Alto desempenho e planejamento financeiro |

- **Cobra por**: leitura e gravação · armazenamento · réplicas globais · streaming · exportação · DynamoDB Streams · transferência (saída de região).
- **Gratuito**: 25 GB (Standard) · 2,5 milhões de leituras do Streams · 100 GB de transferência para a internet, agregados em todos os serviços e regiões da AWS (exceto China e GovCloud).
- **Na POC** (aula 2): a base com a agenda dos eventos.
- **Aula 6, cenário "Dados e análise"**: os **DynamoDB Streams** poderão publicar eventos de gravação, atualização e exclusão, e pode-se escrever um Lambda que gere métricas personalizadas ([[SLS 06 - AWS Lambda e AWS SAM]]).

## Na disciplina Data Engineering (Fase 4)
- Classificado como banco de **chave-valor**, junto com Redis e Riak ([[DE 01 - Fundamentação e SGBDs]], [[DE 03 - Bancos de chave-valor com Redis]]). A aula 3 cita o **Dynamo** (Amazon, 2004) como pioneiro do conceito moderno de chave-valor, sem relacioná-lo ao DynamoDB.
- Como DBaaS: **NoSQL totalmente gerenciado**, **escalável e de baixa latência**, popular para apps móveis e web, jogos e IoT ([[DE 06 - Cloud e DBaaS]]).

Aparece em: [[SLS 01 - Recursos serverless na AWS]], [[SLS 02 - Custos serverless na AWS]], [[SLS 06 - AWS Lambda e AWS SAM]], [[DE 01 - Fundamentação e SGBDs]], [[DE 03 - Bancos de chave-valor com Redis]], [[DE 06 - Cloud e DBaaS]]
