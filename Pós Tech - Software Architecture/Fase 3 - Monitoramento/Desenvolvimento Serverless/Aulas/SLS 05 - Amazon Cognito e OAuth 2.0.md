---
tags: [pos-tech/fase-3, serverless, aws, seguranca, aula]
disciplina: Desenvolvimento Serverless
aula: 5
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 5.pdf (Luiz Zenha)"
---

# SLS 05 - Amazon Cognito e OAuth 2.0

← [[SLS 04 - VPC, Load Balancer e API Gateway]] · [[Desenvolvimento Serverless]] · Próxima → [[SLS 06 - AWS Lambda e AWS SAM]]

> [!summary] Em uma frase
> A nova tarefa: **controlar quem vê os eventos** (inclusive eventos fechados para empresas). A solução, "não exatamente serverless", é o **[[Amazon Cognito]]**, que faz a **identificação e autorização** de usuários. A aula explica o **OAuth 2.0** e seus **três fluxos** e a diferença entre **user pools** (autenticar no app ou na API, emitindo **JWT**) e **identity pools** (credenciais da AWS para acessar recursos).

## Hands On
Usar **grupos de usuários** para gerar o **token JWT** passado na requisição da API:
1. Configurar o **Amazon Cognito**.
2. Criar um **grupo de usuários** e configurá-lo para acesso com **JWT**.
3. Fazer **cadastro e login** para obter o JWT.
4. Integrar e configurar o **API Gateway** ao Cognito.
5. Validar.

Tudo **sem alterar o que já está rodando** (o ECS Fargate, o ALB e o API Gateway das aulas anteriores).

## O Amazon Cognito
- Pode ser usado com outras funcionalidades da AWS ou **integrado via SDK** num aplicativo.
- **Ferramentas prontas**: validação de **e-mail ou telefone** · **MFA** · atributos de cadastro customizados · **grupos** de usuários · administração para **multi tenant** (ex.: B2B, com usuários segregados por cliente) · fluxos de autenticação personalizados · **redes sociais** · **SAML ou OIDC** para acesso **federado**.
- **SDKs** em Java, C++, PHP, Python, Golang, Ruby, .NET e JavaScript. Com o **AWS Amplify**, integra-se a apps **Android, iOS, Flutter** ou **React Native**.

## OAuth 2.0
> [!note] O PDF apresenta o OAuth 2.0 como "um protocolo de **autenticação** muito comum" e, na frase seguinte, como "protocolo padrão da indústria para **autorização**".

- **Protocolo padrão da indústria para autorização**: o usuário acessa recursos de um site **sem expor as credenciais**.
- **Analogia do manobrista**: uma **chave temporária** do carro que só permite dirigir **2 km** para estacionar, sem entregar a chave original. O OAuth cria uma chave especial com **acesso limitado** às informações e por **tempo limitado**.

| Fluxo | Como funciona |
|---|---|
| **Authorization Code Grant** | A aplicação recebe um **código de autorização** e uma **URL de direcionamento**; após a autenticação, o código vai como parâmetro a essa URL e é **trocado pelo token de acesso** (Figura 1) |
| **Implicit Grant** | Os tokens são **expostos diretamente ao usuário final**, com **maior risco** de serem comprometidos antes de expirar. Usar **só se o Authorization Code Grant não puder** ser usado (Figura 2) |
| **Client Credentials Grant** | Para **M2M**: a aplicação se autentica direto com o provedor, **sem interação de usuário**, com um **ID e um Secret** (Figura 3) |

## User pools × identity pools
O Cognito autentica e autoriza usuários do **próprio diretório**, de um **diretório corporativo** (como o **Microsoft AD**) e de provedores como **Google e Facebook**. Tem **dois componentes**, independentes ou em conjunto:

| | User pools (grupo de usuários) | Identity pools (grupo de identidade) |
|---|---|---|
| Quando usar | **Autenticar e autorizar** usuários no **aplicativo ou na API** | **Autorizar** usuários **autenticados ou anônimos** a acessar **recursos da AWS** |
| O que é | Um **diretório de usuários** (criação, gerenciamento, autenticação). Pode ser diretório independente, **provedor de identidade OIDC (IdP)** e **provedor de serviços intermediário (SP)** | **Não exige** um grupo de usuários; aceita declarações autenticadas **direto dos provedores de identidade**. Pode autenticar com um provedor confiável, **como** um user pool ou um serviço **SAML 2.0** |
| O que emite | **JWTs** para um aplicativo, servidor web ou API | **Credenciais da AWS** |
| Autorização | — | **Controle de acesso baseado em função e atributo** |
| Exemplo | Usuário acessa o app, se autentica (com **MFA** se preciso) e recebe o JWT (Figura 4) | Liberar ao time de desenvolvimento funções específicas na conta AWS com o **login corporativo** (Microsoft ou outro compatível com SAML 2.0); o Cognito gera as credenciais conforme a **role** (Figura 5) |

## Referências
AWS: Explorando a concessão Client Credentials do OAuth 2.0 na AWS · Serviço de Autenticação – Customer IAM (CIAM) · What is Amazon Cognito?
