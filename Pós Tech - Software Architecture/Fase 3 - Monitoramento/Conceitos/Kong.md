---
tags: [pos-tech/fase-3, api-gateway, kong, conceito]
aliases: [Kong Gateway, Kong API Gateway, Kong Manager, Kong Konnect, Konnect, Kong Enterprise]
---

# Kong

## Na disciplina API Gateway (Fase 3)
**API Gateway open source** que serve como **proxy para APIs**, com configurações de **autenticação, logs e consumers** ([[APIGW 04 - Conhecendo o Kong]]).

- **Node do Kong Admin**: a API de administração, na porta **8001** no docker compose da aula (`localhost` ou `host.docker.internal`).
- **Consumer**: "o ponto de partida no desenho de arquitetura do Kong". Pode ser usado para autenticar a conexão do **Konga** ao node Admin (Key, JWT, Basic auth) ([[APIGW 04 - Conhecendo o Kong]]). O King gera seu mapa de dependências a partir dos Consumers ([[APIGW 05 - Criando serviços e rotas]]), e no Hands On da aula 6 um consumer, com plugins, **protege as APIs** com **autenticação básica** e **API Key** ([[APIGW 06 - Consumers]]).
- **GUIs**: o **Kong Manager** (pago; free e mais básico desde a **3.4**, sem autenticação) e as da comunidade, [[Konga e King]].
- **Konnect** ([[APIGW 06 - Consumers]]): plataforma de **gerenciamento do ciclo de vida de API** entregue como serviço; **plano de controle** na nuvem do Kong e **plano de dados** no seu ambiente. Inclui **Dev Portal**, **Gateway Manager** e **Mesh Manager** (Kong Mesh).
- **Enterprise × Open Source**: o Enterprise tem **GraphQL** (queries GraphQL → REST, conversão JQ, Rate Limit) e autenticação por **LDAP** e **RBAC**. A Open Source atende **a maioria dos cenários**.

## Na Fase 2
Na [[DK 03 - Orquestração de contêineres]], o **Kong API Gateway com Postgres e migrations** é um dos exemplos de [[Docker Compose]].

## Na disciplina Estrutura de Microsserviços (Fase 4)
- O Kong é o API Gateway do **App FIAP Store** (padrão BFF), configurado graficamente com o **Primate**, com **duas réplicas** do Estoque no Docker Compose, **self-register** no **upstream `estoque`** e **Basic Auth** ([[MS 03 - Gerenciando API com API Gateway e BFF]]).
- Na aula 4, o contrato OpenAPI documenta os endpoints expostos pelo Kong, e o **504 Gateway Timeout** é citado como muito usado por gateways como o Kong ([[MS 04 - Modelo de API para microsserviços]]).

Aparece em: [[APIGW 04 - Conhecendo o Kong]], [[APIGW 05 - Criando serviços e rotas]], [[APIGW 06 - Consumers]], [[MS 03 - Gerenciando API com API Gateway e BFF]], [[MS 04 - Modelo de API para microsserviços]]
