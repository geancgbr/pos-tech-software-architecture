---
tags: [pos-tech/fase-3, serverless, aws, aula]
disciplina: Desenvolvimento Serverless
aula: 4
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 4.pdf (Luiz Zenha)"
---

# SLS 04 - VPC, Load Balancer e API Gateway

← [[SLS 03 - ECS Fargate e ECR]] · [[Desenvolvimento Serverless]] · Próxima → [[SLS 05 - Amazon Cognito e OAuth 2.0]]

> [!summary] Em uma frase
> Dois problemas: **balancear a carga** e **não expor a API por IP**. A solução: o cluster **ECS** e um **Application Load Balancer** numa **subnet privada** de uma **VPC**, e o **API Gateway** como porta de entrada, chegando ao ALB por um **VPC Link**.

## Hands On
1. Criar a **VPC**, as **sub-redes** e os **security groups** (a base do fluxo de acessos).
2. Provisionar o **cluster ECS Fargate**.
3. Criar o **Application Load Balancer** e o **Target Group**.
4. Subir o **serviço no ECS** ligado ao ALB e ao Target Group.

Segundo o resumo, depois foram criados um **VPC Link** e o **AWS API Gateway**, que disponibilizou publicamente um endereço **HTTPS/SSL**.

## Por que uma rede privada
- É preciso uma **visão 360º** do que será construído; **VPC e subnets** são fundamentais em qualquer projeto em cloud.
- A AWS entrega uma **VPC padrão**, bem simples; para **projetos produtivos**, recomenda-se construir uma VPC adequada.
- Peças que devem ficar **protegidas numa rede privada**: um **banco de dados** (exposto publicamente, é risco de invasão gravíssimo, mesmo com senhas fortes) ou uma **API sem segurança nas rotas**, chamada só por outra aplicação (ex.: um front-end em **Django** ou **NextJS**, com sessão e autenticação próprias) pela rede interna. Numa **subnet pública**, alguém poderia descobrir o IP e atacar.
- **O cenário**: expor uma API **sem segurança implementada por enquanto**, que no futuro poderá usar o próprio **API Gateway** para isso.

**Proposta (Figura 1)**: uma **VPC com subnet privada**, com o **cluster ECS** e o **ALB** (que balanceia entre as tasks). O **API Gateway**, com um **VPC Link**, chega à subnet privada e repassa a requisição ao **ALB**, que repassa ao container da API.

## VPC e subnet privada
- **Amazon VPC** (o PDF escreve "Amazon Private Cloud"): uma delimitação de **escopo regional, isolada logicamente**, onde se executam recursos da AWS numa **rede virtual**, com **controle total**: **intervalos de IP**, **sub-redes**, **tabelas de roteamento** e **gateways de rede**.

| Recurso | O que é |
|---|---|
| **Sub-rede** | Um **segmento do intervalo de IPs** da VPC para grupos de recursos isolados (instâncias EC2, cluster) |
| **Internet Gateway** | A **porta de entrada** para a internet pública |
| **NAT Gateway** | Serviço de **NAT** (Network Address Translation) gerenciado e altamente disponível para que recursos de uma **sub-rede privada acessem a internet** |

## Load Balancer
Recebe a requisição e repassa ao serviço **mais livre** e com capacidade de processá-la.

| | Application Load Balancer (ALB) | Network Load Balancer (NLB) |
|---|---|---|
| O que é | O **mais moderno** da AWS | Balanceamento **de rede** |
| Recursos | Exclusivos: **gRPC**, **roteamento baseado na requisição**, **respostas estáticas**, **redirecionamentos de rotas**, **timeout de conexão** | Protocolos **TCP, UDP e TLS**; usa informações da **conexão** |
| Custo | **Ligeiramente mais caro**, por entregar mais | — |

- A aula usa o **ALB**.
- **Target groups** (nos dois tipos): identificam os **alvos (targets)** disponíveis e repassam a requisição ao endereço e à porta deles. Também garantem que os targets estejam **saudáveis**, por **health checks**: ex., um endpoint da API que devolve **200** se estiver tudo certo ou **500** se houver problema (como falha na conexão com o banco). Isso ajuda o **ECS a substituir** a task/container que não está saudável.

## O AWS API Gateway
| Opção | O que o PDF diz |
|---|---|
| **HTTP API** | A **mais recente e mais leve**, para casos **simples**; ideal para **serverless e microsserviços**. Rotas, métodos, integração direta com **Lambda** ou outros serviços HTTP. **Baixa latência e menor custo** que a REST API |
| **REST API** | A **mais antiga**, ainda muito usada. APIs **RESTful completas**: recursos, métodos, modelos de dados, autorização, autenticação, **recursos hierárquicos**, **transformação de dados** e **controle de versão**. Para casos **mais complexos** |
| **WebSocket API** | Comunicação **bidirecional em tempo real** (bate-papos, jogos multiplayer, feeds). Conexões **persistentes**; cliente → servidor e **entre clientes** |

- Para a validação desta aula, a **HTTP API** basta.
- **VPC Link**: uma das opções de integração (HTTP ou REST API), que cria uma conexão com um **Network Load Balancer ou uma VPC**. Permite a integração **segura** de APIs **privadas** numa VPC, com segurança, isolamento e baixa latência.
- **Atenção ao custo**: o VPC Link tem **taxas adicionais**, incluindo transferência de dados dentro e fora da VPC.

## Referências
AWS: Amazon VPC · Elastic Load Balancing · Conceitos básicos do Amazon ECS · API HTTP com integração privada ao ECS · O que é balanceamento de carga?
