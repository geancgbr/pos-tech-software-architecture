---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [API First, Versionamento de API, Versionamento semântico, CORS, OpenAPI, AsyncAPI, Swagger, Códigos de status HTTP, Status code]
---

# Modelagem de APIs

Boas práticas de **documentação e modelagem de APIs** ([[MS 04 - Modelo de API para microsserviços]]).

- **API First**: começar pelo **contrato**, antes dos serviços, para validar e evitar desperdício.
- **Documentação**: **Markdown**, com contratos **OpenAPI** e **AsyncAPI**; **Swagger Editor** e **Swagger UI**.
- **Versionamento**: semântico (`1.0.2`) ou próprio documentado; numa quebra de contrato, manter **as duas versões**; versão por **header**, **URL** (`/v2/`) ou **subdomínio**.
- **Endpoints**: **substantivos** + métodos HTTP (POST criar, PUT atualização total, PATCH parcial, GET obter, DELETE excluir); hierarquia até o **segundo nível**; padrão único de singular ou plural; minúsculas e **hífen**.
- **Query**: paginação, ordenação, seleção de campos.
- **Respostas**: 2xx, 3xx, 4xx, 5xx; 200, 201, **204** (busca vazia), 400, 401/403, **404** (recurso específico inexistente), **429**, 500, 503, 504.
- **Erros**: sem stacktrace; **código + descrição**; 4xx do cliente, 5xx do serviço; tabela de erros.
- **Segurança**: **401 para todos** os cenários de controle de acesso; **404** para endpoints restritos; **OAuth 2.0** em vez de tokens estáticos (dinâmicos expiram normalmente em 5 a 15 min).
- **CORS**: endpoint **OPTIONS** por path com `Access-Control-Allow-Origin` (uma origem; **nunca `*`**), `-Methods` e `-Headers`; o navegador faz o **preflight**.

Aparece em: [[MS 04 - Modelo de API para microsserviços]]
