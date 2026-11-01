---
tags: [pos-tech/fase-4, microsservicos, api, aula]
disciplina: Estrutura de Microsserviços
aula: 4
fonte: "Estrutura de Microsserviços/Estrutura de Microsserviços - Aula 4.pdf"
---

# MS 04 - Modelo de API para microsserviços

← [[MS 03 - Gerenciando API com API Gateway e BFF]] · [[Estrutura de Microsserviços]] · Próxima → [[MS 05 - Implementando queries com microsserviços]]

> [!summary] Em uma frase
> **Documentação e boas práticas de modelagem de APIs**: **API First** (começar pelo contrato), **Markdown** na documentação, **versionamento** (semântico; por header, URL ou subdomínio), endpoints com **substantivos** e métodos HTTP, parâmetros **query**, **códigos de resposta**, **tratamento de erros**, **segurança** (401 em todos os cenários de controle de acesso; 404 para endpoints restritos; OAuth 2.0) e **CORS**. Ver [[Modelagem de APIs]].

## Hands On
Criar o contrato da API **"FIAP Store – Website"** com os endpoints do Estoque expostos pelo **Kong**:
- Subir os containers do Estoque e do Kong da aula anterior e usar o **Primate** para ver a API configurada.
- No **Swagger Editor**, partir do contrato **OpenAPI 3.0** de exemplo da **Petstore**.
- Executar o `POST /estoque` pela interface do Swagger Editor; especificar o **security schema** (o **Basic Auth** configurado) e ver o que acontece ao cadastrar um produto **só com o SKU**.
- Especificar os outros endpoints e publicar o contrato no **Swagger UI**.
- Segundo o resumo, a aula trata dos padrões **OpenAPI** e **AsyncAPI** para a documentação.

## API First
Começar pela **modelagem do contrato** da API, **antes** de desenvolver os serviços, para validar se atende aos clientes e **evitar desperdício** de desenvolvimento.

## Markdown
- Sintaxe simples para formatar a documentação. **Seções** com `#`: `# Seção 1.`, `## Seção 1.1.`, `# Seção 2.`. É preciso um **espaço** depois do `#` (`#Título` não vira seção).
- **Negrito**: `**texto**` ou `__texto__`. **Itálico**: `*texto*` ou `_texto_`. Também há código, tabelas, links e imagens.
- Compatível com os contratos **OpenAPI** e **AsyncAPI**, em arquivos `.yaml`, `.json`, `.md`, `.txt`.

## Versionamento
- Comunica aos clientes as alterações (correções, funcionalidades, **depreciações**). Ex.: o **versionamento semântico** (formato `1.0.2`), "um dos mais utilizados mundialmente". Um padrão próprio também é possível, **desde que documentado**.
- **Mudança que quebra o contrato** (ex.: `/estoque` → `/estoques`, mudança no JSON do body): manter **a versão antiga e a nova** em produção, dando **tempo hábil** aos clientes.
- O cliente escolhe a versão, e o API Gateway pode lê-la por:
  - **Header**: `Accept: application/json; Version=2`
  - **URL**: `https://api.fiapstore.com.br/v2/`
  - **Subdomínio**: `https://v2.api.fiapstore.com.br/`

## Endpoints
- Usar **substantivos** que representem o recurso; **evitar verbos**: a ação vem do **método HTTP**.

| Método | Significado | Exemplo |
|---|---|---|
| **POST** | Criar | `POST /produto` |
| **PUT** | Atualização **total** (campo omitido é **apagado**) | `PUT /produto/{sku}` |
| **PATCH** | Atualização **parcial** | `PATCH /produto/{sku}` |
| **GET** | Obter | `GET /produto/{sku}` · `GET /produto?categoria=10` |
| **DELETE** | Excluir | `DELETE /produto/{sku}` |

- **Hierarquia**: o autor recomenda **até o segundo nível** (ex.: `GET /produto/{sku}/relatorio/{ano}` em vez de `.../relatorio/venda/{ano}`; o tipo vai em parâmetro).
- **Singular ou plural**: escolher **um padrão**, de preferência para todas as APIs da empresa. Tudo em **minúsculo**, palavras separadas por **hífen** (`GET /preco-lista`).

**Parâmetros query**: paginação (`?pagina=1&qtd_itens=10`) · ordenação (`?ordena=nome`) · seleção de campos (`?campos=nome,url_imagem`), combináveis.

## Respostas
**Classes**: **2xx** sucesso · **3xx** redirecionamento · **4xx** erro no cliente · **5xx** erro no servidor.

| Código | Uso |
|---|---|
| **200 OK** | Processada com sucesso |
| **201 Created** | Recurso criado |
| **204 No Content** | Sucesso **sem conteúdo**; normalmente em **buscas** sem resultado |
| **400 Bad Request** | Parâmetros errados ou faltando |
| **401 Unauthorized** | Credencial inválida, token expirado ou sem autorização (alternativamente, **403 Forbidden**) |
| **404 Not Found** | O recurso **específico** não existe (diferente do 204, é **erro**) |
| **429 Too Many Requests** | O serviço não pôde receber a requisição, "independente do motivo" |
| **500 Internal Server Error** | Falha interna, sem relação com a requisição (bugs, integrações) |
| **503 Service Unavailable** | Serviço indisponível (ex.: o banco caiu) |
| **504 Gateway Timeout** | Serviço inacessível; muito usado por **proxies reversos** (Apache, Nginx) e **API Gateways** (Kong) |

> [!note] Na tabela, o 403 Forbidden aparece como alternativa ao 401; na seção de segurança, a recomendação é padronizar o 401 para todos os cenários de controle de acesso, mas, logo depois, usar o 404 para endpoints que o usuário não está autorizado a consumir.

## Tratamento de erros
- **Não enviar stacktrace** nem detalhes da tecnologia (evita expor informação a atacantes).
- Mensagem **padronizada** com **código** e **descrição**:
  ```json
  { "erro": { "codigo": "produto.id.invalido", "descricao": "ID de produto inválido. Formato suportado: string." } }
  ```
- **4xx** para erros do cliente, **5xx** para erros do serviço, e uma **tabela de erros** referenciada no contrato.

## Segurança
- **Padronizar o 401** em todos os cenários de controle de acesso: 401 para credencial inválida e **403** para válida-mas-sem-acesso dá **dicas** ao atacante de que a credencial é válida.
- Para endpoints restritos (ex.: só **"role admin"**), usar **404 Not Found** para indicar que o endpoint "não existe".
- **Evitar tokens estáticos** (sobretudo em apps e sites públicos); preferir o **OAuth 2.0**. Um token **dinâmico** expira (normalmente **entre 5 e 15 minutos**), limitando o estrago de um roubo.

## CORS
- Indica às aplicações clientes (como **navegadores**) quais requisições e respostas estão **autorizadas**; uma requisição diferente é **interrompida pelo próprio cliente**.
- **Exemplo do ataque**: um e-mail falso leva ao site **"fiapstor.com.br"** (sem o "e"), idêntico ao original e usando a API da FIAP Store; no pagamento, o site troca a API para o usuário **pagar ao atacante**. Possível sem um **CORS adequado**.
- Para cada **path** (`/produto`, `/produto/{sku}`, `/estoque`), definir um endpoint **OPTIONS** com os headers CORS (ex.: `OPTIONS /produto`).
- Os navegadores **implementam CORS nativamente** (não dá para desligar num site React ou Angular). Requisições qualificadas geram uma requisição **"preflight"** antes da desejada.

| Header | O que indica |
|---|---|
| `Access-Control-Allow-Origin` | A **origem** autorizada (ex.: `https://fiapstore.com.br`). Só **uma** por resposta: com várias origens, o serviço avalia o header `Origin` e devolve a específica. **Não usar `*`** |
| `Access-Control-Allow-Methods` | Os **métodos** autorizados (ex.: `GET, POST`) |
| `Access-Control-Allow-Headers` | Os **headers** autorizados (ex.: `Content-Type, Authorization`) |

## Referências
Google Cloud: API design guide · AsyncAPI Specification 2.6.0 · Swagger: Best Practices in API Design · Apigee: Build RESTful APIs · OpenAPI Specification v3.1.0 · Microsoft: RESTful web API design · Swagger: What Is OpenAPI?
