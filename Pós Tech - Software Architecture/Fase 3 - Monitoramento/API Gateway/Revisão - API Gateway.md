---
tags: [pos-tech/fase-3, api-gateway, revisao]
disciplina: API Gateway
---

# Revisão - API Gateway

[[API Gateway]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução ao API Gateway
> [!question]- O que é um API Gateway?
> Um componente intermediário que é o ponto de entrada de todas as chamadas de API: um "guardião" que direciona as solicitações e coordena as respostas; um único ponto de contato para várias APIs. → [[APIGW 01 - Introdução ao API Gateway]]

> [!question]- Quais os benefícios do API Gateway citados?
> Consolidação e simplificação, segurança, monitoramento e análise, transformação de dados e cache.

> [!question]- Como o pico de acesso do debate presidencial foi resolvido?
> Como tudo apontava para o GW, fizeram apontamentos para uma estrutura com Kubernetes, replicando as APIs em muitos Pods, sem publicar novamente o site, sem derrubar os usuários e sem ter que replicar o aplicativo.

> [!question]- O que um gateway real teria além do Hands On?
> Autenticação, limitação de requests e balanceamento de carga, entre outras.

## Aula 2 - API Management do Azure
> [!question]- O que é o Azure API Management?
> Um serviço em nuvem do Azure para criar, gerenciar e expor APIs de forma eficaz e segura, atuando como gateway central das APIs da organização. → [[Azure API Management (APIM)]]

> [!question]- Cite recursos do APIM.
> Portal do Desenvolvedor, gateways distribuídos, políticas e transformações, versionamento, segurança, monitoramento, portal de administrador, integração com serviços Azure, cache, OpenAPI/Swagger e gerenciamento de tráfego.

> [!question]- Em qual tier o Portal do Desenvolvedor não se aplica?
> No Consumption Plan.

> [!question]- Como o APIM ajuda no exemplo dos pagamentos de vários fornecedores?
> Cria APIs unificadas e padronizadas e cuida de autenticação, transformação de dados e segurança, com análises do uso.

## Aula 3 - APIM na prática
> [!question]- O que são políticas de API?
> Conjuntos de regras e ações aplicadas a uma API, intermediárias entre solicitações e respostas, que controlam como os dados são tratados, transformados e protegidos. → [[Políticas de API]]

> [!question]- Como exigir uma chave para acessar uma API no APIM?
> Em "Políticas de Segurança", selecionar "Chave de assinatura" (e, nas políticas de entrada, "Verificar chave de consulta ou cabeçalho").

> [!question]- Quais métricas são vitais no monitoramento do APIM?
> Tráfego da API, tempo de resposta, taxas de erro, latência e taxas de uso por recurso.

> [!question]- Quais os benefícios do cache no APIM?
> Melhoria do desempenho, redução da latência, economia de recursos e escalabilidade.

> [!question]- Por que o monitoramento não é só reativo?
> Porque também é preventivo: identifica problemas antes que virem interrupções e orienta otimização, escalabilidade e planejamento.

## Aula 4 - Kong e Konga
> [!question]- O que é o Kong?
> Um API Gateway open source que serve como proxy para APIs, com configurações de autenticação, logs e consumers. → [[Kong]]

> [!question]- O que mudou no Kong Manager na versão 3.4?
> Passou a ter uma versão free, mais básica e sem autenticação, mas com o core de funcionalidades.

> [!question]- Konga × King?
> Konga: server side, com login e banco de dados. King: client side, sem login, configuração local. → [[Konga e King]]

> [!question]- Quais os três campos exclusivos do Konga?
> Users, Snapshots e Settings.

## Aula 5 - King
> [!question]- O que o King gera, e com base em quê?
> Um mapa de dependências baseado em Consumers, o ponto de partida no desenho de arquitetura do Kong.

> [!question]- Por que o Konga é considerado superior ao King?
> Entrega mais funcionalidades e permite controle de acesso; o King é client side e não tem login.

## Aula 6 - Konnect e Enterprise
> [!question]- O que é o Kong Konnect?
> Uma plataforma de gerenciamento do ciclo de vida de API entregue como serviço: plano de controle na nuvem do Kong e plano de dados no seu ambiente. → [[Kong]]

> [!question]- Para que servem o Dev Portal, o Gateway Manager e o Mesh Manager?
> Dev Portal: devs localizam, testam e consomem APIs. Gateway Manager: catalogar, conectar e monitorar planos de controle e nós do plano de dados. Mesh Manager: malhas Kong Mesh.

> [!question]- O que o Kong Enterprise tem que o Open Source não tem?
> GraphQL (queries para REST, conversão JQ, Rate Limit) e autenticação por LDAP e RBAC, entre outras.

## Dúvidas em aberto
- Aula 3: o texto diz "trabalhar com OpenAI", mas explica a importação por OpenAPI.
- Aula 2: o resumo diz que o APIM "conseguiu garantir a audiência" da emissora; o Saiba Mais só diz que ele "foi utilizado" no caso, e a aula 1 credita a audiência à parceria com o Google.
- Aula 4: o Saiba Mais diz que as funcionalidades do Konga são "idênticas" às do Kong Manager; o resumo diz que "são diferentes".
- Aula 5: o título é "Criando serviços e rotas", mas o conteúdo é o King; o container publica a porta 4200, mas o texto manda abrir `localhost:4500`.
- Aula 6: o título é "Consumers", mas o texto trata do Konnect e da versão Enterprise.

## Pontos fracos (o que errei)
