---
tags: [pos-tech/fase-3, api-gateway, azure, aula]
disciplina: API Gateway
aula: 2
fonte: "API Gateway/2 - Introduçao ao APIM_revFinal.pdf (Milton Camara)"
---

# APIGW 02 - API Management do Azure

← [[APIGW 01 - Introdução ao API Gateway]] · [[API Gateway]] · Próxima → [[APIGW 03 - API Management na prática]]

> [!summary] Em uma frase
> O **[[Azure API Management (APIM)]]** é um serviço em nuvem da Microsoft para **criar, gerenciar e expor APIs** de forma eficaz e segura, atuando como **gateway central** de todas as APIs da organização. Segundo o PDF, foi ele o gateway usado no caso da emissora.

## Hands On (vídeo)
Criar um recurso do **Azure API Management** e publicar uma **API de exemplo**. O texto convida para a "aula prática em vídeo".
1. **Portal do Azure** (portal.azure.com) → **"Criar um recurso"** → buscar **"API Management"** → **"Criar"**.
2. Preencher **assinatura, grupo de recursos, nome único, localização** (próxima dos usuários) e **nível de precificação** (para teste, **"Development"**). **"Revisar + Criar"** → **"Criar"**.
3. No recurso: **"APIs"** → **"Adicionar API"** → **"API de exemplo"** (pré-construída para teste) → **"Criar"**.
4. **Testar**: na API, **"Testar"** → método **GET** → **"Enviar"**.
5. **Portal do desenvolvedor** (**não se aplica ao tier Consumption Plan**): ver APIs publicadas, documentação e mais.
6. **Limpeza**: se for só teste, **deletar** o recurso para evitar custos.

## O que é o APIM
- Uma solução abrangente da Microsoft para **criação, publicação, proteção e monitoramento** de APIs.
- Serviço em nuvem do **Microsoft Azure** para **criar, gerenciar e expor APIs** de maneira eficaz e segura.
- Atua como **gateway central** de todas as APIs da organização, publicando APIs **internas e externas** de forma controlada e padronizada.

## Recursos
| Recurso | O que o PDF diz |
|---|---|
| **Portal do Desenvolvedor** | Portal interativo para descobrir, testar e consumir APIs: documentação, exemplos de código, **sandbox** e depuração |
| **Gateways** | Gateways **distribuídos globalmente** para desempenho e disponibilidade |
| **Gerenciamento de API** | Criar, importar e gerenciar APIs: definições, esquemas, políticas de segurança, transformações |
| **Políticas e Transformações** | Segurança, autenticação, autorização, **limitação de taxa** e transformações |
| **Versionamento** | Várias **versões** de APIs, para mudanças controladas |
| **Segurança** | Autenticação, autorização, **tokens de acesso** e **certificados** |
| **Análises e Monitoramento** | Tráfego, padrões de uso, gargalos, insights |
| **Portal de Administrador** | Gerenciar políticas, usuários, **assinaturas** |
| **Integração com outros serviços Azure** | **Azure Functions, Logic Apps, Event Grid, Azure Active Directory** |
| **Publicação e Distribuição** | Gateway seguro e escalável para uso interno ou externo |
| **Integração com Mercados** | Listar APIs no **Azure Marketplace** ou outros |
| **Cache** | Respostas em cache: desempenho e menos carga |
| **Suporte a OpenAPI e Swagger** | Importar, exportar e gerar especificações **OpenAPI (antes Swagger)** |
| **Gerenciamento de Tráfego** | Distribuição inteligente entre **versões** ou **back-ends** |

## Benefícios
1. **Centralização e padronização** de desenvolvimento, autenticação, autorização e segurança.
2. **Gateway de entrada** para todas as chamadas, com monitorização, análise e otimização do tráfego.
3. **Segurança robusta**, consistente em todas as APIs.
4. **Transformação de dados** de entrada e saída.
5. **Analytics e insights**: tráfego, tempos de resposta, erros, padrões de uso.

## Exemplo: pagamentos de vários fornecedores
- Um **aplicativo móvel** integra serviços de **pagamento** de fornecedores diferentes, cada um com sua **autenticação** e **estrutura de dados**. Usá-los **diretamente** seria complexo (Figura 1).
- Com o APIM, a empresa cria **APIs unificadas e padronizadas**; o APIM cuida de **autenticação, transformação de dados e segurança**, e dá **análises** do uso (Figura 2).

> [!note] O "O que vem por aí" diz que o APIM resultou num "aumento considerável na audiência" da emissora, e o resumo diz que ele "conseguiu garantir a audiência". O Saiba Mais só diz que ele "foi utilizado" no caso, e a aula 1 credita a audiência à parceria com o Google; o gateway entra para aguentar o pico.

> [!note] O título interno do PDF é "API Management do Azure"; o nome do arquivo é "Introdução ao APIM".

## Referências
Bachina (2021, 2022): Azure APIM com Function App, Cosmos DB e Terraform · Auth 2.0 no APIM · Azure FrontDoor com APIM
