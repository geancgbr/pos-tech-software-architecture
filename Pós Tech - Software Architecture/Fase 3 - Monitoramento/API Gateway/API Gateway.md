---
tags: [pos-tech/fase-3, api-gateway, indice]
disciplina: API Gateway
fase: 3
aulas: 6
aliases: [API GW, APIGW, GW]
---

# API Gateway

[[Fase 3 - Monitoramento]] · Revisão → [[Revisão - API Gateway]]

Autores dos PDFs: **Milton Camara** (aulas 1 a 3) e **Douglas Lima da Silva Martins** (aulas 4 a 6).

> [!summary] O que é um API Gateway, segundo a aula 1
> Um **componente intermediário** que atua como **ponto de entrada para todas as chamadas de API**: um "guardião" que direciona as solicitações dos clientes aos serviços subjacentes e coordena as respostas. Em essência, **um único ponto de contato para várias APIs**. Benefícios: **consolidação, segurança, monitoramento, transformação de dados e cache**.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[APIGW 01 - Introdução ao API Gateway]] | API Gateway, o caso do debate presidencial |
| 2 | [[APIGW 02 - API Management do Azure]] | [[Azure API Management (APIM)]] |
| 3 | [[APIGW 03 - API Management na prática]] | [[Políticas de API]], [[Estratégias de Cache]] |
| 4 | [[APIGW 04 - Conhecendo o Kong]] | [[Kong]], [[Konga e King]] |
| 5 | [[APIGW 05 - Criando serviços e rotas]] | [[Konga e King]] (King) |
| 6 | [[APIGW 06 - Consumers]] | [[Kong]] (Konnect, Enterprise) |

## As ferramentas da disciplina
| Ferramenta | Tipo | Aulas |
|---|---|---|
| Gateway em **.NET Core 7** | Implementação simples (Hands On) | 1 |
| **[[Azure API Management (APIM)]]** | Serviço em nuvem da Microsoft | 2 e 3 |
| **[[Kong]]** | Open source (e Enterprise, Konnect) | 4 a 6 |
| **[[Konga e King]]** | GUIs da comunidade para o Kong | 4 e 5 |

## Ligações com outras disciplinas
- **Kubernetes (Fase 2)**: no caso da emissora, o pico foi resolvido replicando as APIs em muitos [[Pod|Pods]] no Kubernetes, apontados pelo gateway.
- **Dockerização (Fase 2)**: o Kong já aparece como exemplo de [[Docker Compose]] na [[DK 03 - Orquestração de contêineres]]; aqui, Konga e King sobem com Docker.
- **Arquitetura de Software (Fase 1)**: cache em [[Estratégias de Cache]].

## Amazon API Gateway (disciplina Desenvolvimento Serverless)
Na Fase 3, o **Amazon API Gateway** aparece como "a grande estrela" da migração serverless: criar, publicar, monitorar e proteger APIs, com opções **HTTP, REST e WebSocket**, **VPC Link** e integração com o [[Amazon Cognito]]. Ver [[SLS 01 - Recursos serverless na AWS]], [[SLS 02 - Custos serverless na AWS]], [[SLS 04 - VPC, Load Balancer e API Gateway]] e [[SLS 05 - Amazon Cognito e OAuth 2.0]].

## Na disciplina Estrutura de Microsserviços (Fase 4)
O padrão **API Gateway** desacopla clientes e serviços e pode implementar Service Discovery, Circuit Breaker e API Composition, além de segurança, **rate limit** (backpressure, HTTP 429), cache e métricas, com uma plataforma de **API Management**. Ver [[MS 03 - Gerenciando API com API Gateway e BFF]].

## Material
PDFs em `~/Desktop/API Gateway/` ("1 - Introdução ao APIGW_revFinal.pdf", "2 - Introduçao ao APIM_revFinal.pdf", "3 - APIM na Prática_revFinal.pdf" e "POSTECH - Aula4/5/6_revFinal.pdf").
