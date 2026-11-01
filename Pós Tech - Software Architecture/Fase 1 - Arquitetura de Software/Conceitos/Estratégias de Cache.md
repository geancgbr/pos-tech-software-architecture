---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Cache, Estratégia de cache]
---

# Estratégias de Cache

O cache **armazena temporariamente em memória os dados acessados com frequência**, para não buscá-los de novo na origem (banco de dados, sistema de arquivos). Isso reduz o tempo de busca e processamento e melhora a velocidade de resposta.

| Estratégia | O que fica em cache | Efeito |
|---|---|---|
| **Página inteira** | A página toda: HTML, CSS, JS e outros recursos | Melhora bastante o tempo de carregamento |
| **Banco de dados** | Dados muito acessados, como o perfil do usuário | Menos requisições ao banco |
| **Objeto** | Objetos complexos ou recursos muito usados (imagens, JSON) | Não se aplica |
| **Sessão** | Preferências, histórico de navegação, carrinho | Melhora o desempenho |
| **CDN** | Mídia (imagens, vídeos) em servidores distribuídos pelo mundo | O usuário acessa o servidor mais próximo, com menos tempo de resposta |

O fluxo de cache está na Figura 1 do PDF da aula 4.

Na aula 5, uma **porta de cache** com dois adaptadores (Redis e cache em memória) ilustra as [[Portas e Adaptadores|portas e adaptadores]].

## Na disciplina API Gateway (Fase 3)
- O **cache de respostas de API** no gateway pode melhorar o desempenho, reduzir a carga nos serviços e acelerar as respostas para solicitações frequentes ([[APIGW 01 - Introdução ao API Gateway]]).
- No **APIM**, o cache é o armazenamento **temporário** de dados acessados com frequência, aplicado às **respostas das APIs**. Benefícios: desempenho, menos latência, economia de recursos e escalabilidade ([[APIGW 03 - API Management na prática]]).

Aparece em: [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], [[ARQ 05 - Arquitetura Hexagonal]], [[APIGW 01 - Introdução ao API Gateway]], [[APIGW 03 - API Management na prática]]
