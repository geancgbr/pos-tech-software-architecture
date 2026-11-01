---
tags: [pos-tech/fase-3, serverless, aws, aula]
disciplina: Desenvolvimento Serverless
aula: 2
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 2.pdf (Luiz Zenha)"
---

# SLS 02 - Custos serverless na AWS

← [[SLS 01 - Recursos serverless na AWS]] · [[Desenvolvimento Serverless]] · Próxima → [[SLS 03 - ECS Fargate e ECR]]

> [!summary] Em uma frase
> A empresa de ingressos monta uma **POC**: um **DynamoDB** com a agenda de eventos e uma **API GET** para o front-end. Como o **Lambda** não expõe uma API RESTful sozinho, entra o **API Gateway**. A aula explica a **cobrança** de **Lambda, API Gateway e DynamoDB** e usa a **AWS Pricing Calculator**: cerca de **17,98 USD/mês** (215,76 USD/ano).

> [!note] O PDF não traz título; o nome desta nota descreve o conteúdo.

## Hands On
Navegar pelos produtos, explorar os detalhes de **cobrança** e usar a **AWS Pricing Calculator** para estimar o custo da POC.

## A POC
- Fluxo da Figura 1: **API Gateway** recebe as requisições e repassa ao **Lambda**, que consulta o **banco de dados** (DynamoDB). "Por si só a Lambda não é capaz de expor uma API RESTful".
- Por isso, o custo precisa incluir mais do que a função Lambda.

## Custos do Lambda
Ver [[AWS Lambda]].
| Item | Como é cobrado |
|---|---|
| **Solicitação** | Contada sempre que a função começa a executar em resposta a um acionador (ex.: **SNS** ou chamada do **API Gateway**) |
| **Duração** | Do início da execução até retornar ou encerrar, arredondada para o **1 ms*** mais próximo (o asterisco está no PDF). O custo depende da **memória** configurada: **mais memória, maior o preço base** |
| **Nível gratuito** | **1 milhão de solicitações/mês** e **400.000 GB-segundos/mês** |
| **Arquitetura** | **x86** ou **ARM**, com tabelas diferentes (Figuras 2 a 4; a Figura 2 é uma função com 1024 MB) |
| **Casos específicos** | Armazenamento temporário ou **Lambdas previamente provisionadas** (para melhorar o tempo de resposta) têm outros cálculos |

- Como o custo depende do **tempo de execução**, as Lambdas devem ser **simples e otimizadas**.

## Custos do API Gateway
- Opções **HTTP, REST e WebSocket**, cada uma com custo e cálculo diferentes.

| | REST | HTTP |
|---|---|---|
| Recursos | **Mais completos**, como um **proxy** na frente da aplicação: **chaves de API**, **limitação por cliente**, **validação de solicitações**, integração com o **AWS WAF**, **endpoints privados** | **Mais simples** |
| Custo | Maior | **Menor** |

- Cobrança pela **quantidade de chamadas**, com **free tier de 1 milhão de chamadas/mês** (Figura 5).
- **Cache** das requisições é **opcional** e tem **custo à parte** (Figura 6).

## Custos do DynamoDB
Ver [[Amazon DynamoDB]].
- Totalmente gerenciado: **segurança integrada, backups, replicação multirregional, cache em memória** e importação e exportação.

| Modo | Como funciona | Vantagem |
|---|---|---|
| **On-demand capacity** | **Paga pelo uso** | Ambientes ainda **imprevisíveis** |
| **Provisioned capacity** | Especifica o **número de leituras e escritas** esperadas | **Alto desempenho** garantido e **planejamento financeiro** |

- **Cobranças**: leitura e gravação · dados armazenados · réplicas globais · streaming · exportação · DynamoDB Streams · transferência de dados (saída de região).
- **Uso gratuito**: **25 GB** (DynamoDB Standard) · **2,5 milhões** de leituras do Streams · **100 GB** de transferência para a internet, agregados em todos os serviços e regiões (exceto China e GovCloud).

## AWS Pricing Calculator
- Estima os custos de infraestrutura, **serverless ou não** (calculator.aws). Cuidado com a **região**: os valores mudam.
- **Dados da POC**: a página da agenda tem em média **3.000.000 acessos/mês**; a requisição é simples, **não paginada**, com os eventos dos **próximos 30 dias**; as informações dos eventos ocupam no máximo **1 KB**; em média **20 eventos/mês**.
- **Resultado**: cerca de **17,98 USD por mês** (**215,76 USD por ano**), **sem considerar o free tier** do primeiro ano.

## Referências
AWS: Definição de preço do AWS Lambda · Preço do Amazon API Gateway · Preço do Amazon DynamoDB · Sem servidor na AWS · Calculadora de preços da AWS
