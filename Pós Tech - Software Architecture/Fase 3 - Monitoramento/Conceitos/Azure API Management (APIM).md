---
tags: [pos-tech/fase-3, api-gateway, azure, conceito]
aliases: [APIM, Azure APIM, API Management, Portal do Desenvolvedor]
---

# Azure API Management (APIM)

Serviço em nuvem do **Microsoft Azure** para **criar, gerenciar e expor APIs** de forma eficaz e segura. Atua como **gateway central** de todas as APIs da organização, internas e externas ([[APIGW 02 - API Management do Azure]]).

- **Recursos**: Portal do Desenvolvedor · gateways distribuídos globalmente · gerenciamento de API · [[Políticas de API|políticas e transformações]] · versionamento · segurança (tokens, certificados) · análises e monitoramento · portal de administrador · integração com Azure Functions, Logic Apps, Event Grid e Azure AD · publicação · Azure Marketplace · cache · **OpenAPI/Swagger** · gerenciamento de tráfego.
- **Benefícios**: centralização e padronização · gateway de entrada · segurança robusta · transformação de dados · analytics.
- **Portal do Desenvolvedor**: onde os devs descobrem, testam e consomem as APIs (documentação, exemplos, sandbox). **Não se aplica ao tier Consumption Plan**.
- **Na prática** ([[APIGW 03 - API Management na prática]]): API manual ("API em branco" + Web Service URL), **chave de assinatura**, política "Verificar chave de consulta ou cabeçalho", **Monitoramento** e **Alertas**, **Cache** e testes no Portal do Desenvolvedor.
- **Métricas de monitoramento**: tráfego, tempo de resposta, taxas de erro, latência e uso por recurso.
- Segundo o PDF da aula 2, foi o gateway usado no caso da emissora ([[APIGW 01 - Introdução ao API Gateway]]).

Aparece em: [[APIGW 02 - API Management do Azure]], [[APIGW 03 - API Management na prática]]
