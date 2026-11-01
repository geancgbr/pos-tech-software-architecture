---
tags: [pos-tech/fase-3, serverless, aws, seguranca, conceito]
aliases: [Cognito, AWS Cognito, User pools, Identity pools, OAuth 2.0, OAuth, OAuth2.0, Authorization Code Grant, Implicit Grant, Client Credentials Grant]
---

# Amazon Cognito

Serviço da AWS que faz a **identificação e autorização de usuários**. Segundo a aula, "não exatamente serverless" ([[SLS 05 - Amazon Cognito e OAuth 2.0]]).

- **Recursos**: validação de e-mail ou telefone · **MFA** · atributos customizados · **grupos** · **multi tenant** (B2B) · fluxos personalizados · redes sociais · **SAML ou OIDC** (acesso federado). SDKs em várias linguagens e, com o **AWS Amplify**, em apps Android, iOS, Flutter e React Native.

| | User pools | Identity pools |
|---|---|---|
| Para | Autenticar e autorizar no **app ou na API** | Autorizar usuários autenticados ou **anônimos** a acessar **recursos da AWS** |
| Emite | **JWTs** | **Credenciais da AWS** |

## OAuth 2.0
**Protocolo padrão da indústria para autorização**: acesso a recursos **sem expor as credenciais**, como uma **chave temporária** do carro dada ao manobrista.

| Fluxo | Resumo |
|---|---|
| **Authorization Code Grant** | Código de autorização + URL de direcionamento; o código é trocado pelo token |
| **Implicit Grant** | Tokens expostos ao usuário final; usar só se o anterior não for possível |
| **Client Credentials Grant** | **M2M**, sem usuário, com **ID e Secret** |

- **No Hands On**: um grupo de usuários gera o **JWT** passado na requisição, e o **API Gateway** é configurado para exigir autenticação.
- Na Fase 3, o OAuth também aparece como forma de autenticação nas [[Políticas de API]] do APIM ([[APIGW 03 - API Management na prática]]).

Aparece em: [[SLS 05 - Amazon Cognito e OAuth 2.0]]
