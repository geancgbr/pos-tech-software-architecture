---
tags: [pos-tech/fase-4, microsservicos, revisao]
disciplina: Estrutura de Microsserviços
---

# Revisão - Estrutura de Microsserviços

[[Estrutura de Microsserviços]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Monolito e microsserviços
> [!question]- O que é uma arquitetura monolítica?
> Um único componente executável (.exe, .war), com todos os módulos no mesmo processo, compartilhando classes e banco de dados. → [[Arquitetura Monolítica]]

> [!question]- Quais os desafios do monolito quando ele cresce?
> O time-to-market diminui (com perda de competitividade, segundo o PDF), menos autonomia das squads, muitos merges, complexidade, IDE lenta, escala cara, menor confiabilidade (uma exceção derruba tudo) e stack obsoleta.

> [!question]- O que define a arquitetura de microsserviços?
> Serviços fracamente acoplados, cada um com sua API e seu banco (logicamente dedicado), evoluindo e escalando de forma independente. → [[Arquitetura de Microsserviços]]

> [!question]- O que é um monolito distribuído?
> O resultado de uma decomposição errada: traz as desvantagens das duas arquiteturas.

> [!question]- Quando adotar microsserviços?
> De forma gradual, quando a aplicação cresce e as desvantagens do monolito aparecem; no início, não há problemas que os microsserviços resolvam.

> [!question]- Quais as 3 camadas dos padrões de microsserviços?
> Padrões de aplicação, de infraestrutura de aplicação e de infraestrutura.

## Aula 2 - Comunicação
> [!question]- Quais os estilos de comunicação one-to-one e one-to-many?
> One-to-one: request/response síncrono, request/response assíncrono e notificação one-way. One-to-many: publish/subscribe e publish/async response. → [[Estilos de Comunicação entre Serviços]]

> [!question]- Quais os desafios de uma API síncrona?
> Só request/response, menor disponibilidade, lentidão propagada ao cliente e a necessidade de conhecer as URLs dos serviços.

> [!question]- Quais os estados do Circuit Breaker?
> Fechado (normal), aberto (interrompe as chamadas) e semi-aberto (testa algumas chamadas). → [[Circuit Breaker]]

> [!question]- Descoberta client-side × server-side?
> Client-side: o cliente consulta o registry e balanceia. Server-side: um roteador intermediário consulta e roteia. → [[Descoberta de Serviços]]

> [!question]- Quantas horas por ano fica indisponível um serviço com 99%?
> 1% × 365 × 24 = 87,6 horas.

> [!question]- O que pode ir no body de uma mensagem, e quais os tipos de canal?
> Documento, comando ou evento. Canais point-to-point (um destinatário) e publish-subscribe (cópia para cada inscrito), num broker como o Kafka.

## Aula 3 - API Gateway e BFF
> [!question]- Que padrões o API Gateway pode implementar?
> Service Discovery, Circuit Breaker e, dependendo da solução, API Composition. → [[MS 03 - Gerenciando API com API Gateway e BFF]]

> [!question]- O que é backpressure no rate limit?
> Ao ultrapassar a taxa configurada, o gateway interrompe as novas requisições e devolve HTTP 429 Too Many Requests.

> [!question]- Quais as desvantagens do API Gateway?
> Mais um componente para sustentar, ponto central (se cair, para tudo; prever alta disponibilidade) e toda mudança precisa ser refletida nele.

> [!question]- O que é o BFF, e quais as vantagens?
> Um backend para cada interface de usuário, com um API Gateway dedicado ao cliente: entrega só os dados necessários, uma squad responsável, custos previsíveis, instância mais leve e métricas segmentadas. → [[Backend for Frontend (BFF)]]

## Aula 4 - Modelagem de APIs
> [!question]- O que é API First?
> Começar pela modelagem do contrato da API antes de desenvolver os serviços. → [[Modelagem de APIs]]

> [!question]- Como o cliente pode escolher a versão da API?
> Por header (`Accept: application/json; Version=2`), URL (`/v2/`) ou subdomínio (`v2.api...`).

> [!question]- PUT × PATCH?
> PUT: atualização total (campo omitido é apagado). PATCH: atualização parcial.

> [!question]- 204 × 404?
> 204: sucesso, mas a busca não encontrou nada. 404: o recurso específico não existe (erro).

> [!question]- Por que padronizar o 401 em todos os cenários de acesso?
> Para não dar dicas ao atacante de que uma credencial é válida (como aconteceria com 401 e 403 separados).

> [!question]- Para que serve o CORS, e por que não usar `*`?
> Indica aos clientes (navegadores) o que está autorizado, bloqueando requisições não autorizadas; `*` autorizaria qualquer origem, inclusive atacantes.

## Aula 5 - Queries
> [!question]- Por que o banco compartilhado é um anti-pattern em microsserviços?
> Porque não garante o baixo acoplamento entre serviços. → [[Banco de Dados por Serviço]]

> [!question]- API Composition × CQRS: qual preferir?
> Normalmente o API Composition, pela facilidade de uso (as chamadas podem ser paralelizadas para reduzir a latência); se os desafios dele inviabilizarem, o CQRS. → [[API Composition]]

> [!question]- Quais os cuidados com Event Handlers no CQRS?
> Idempotência, consistência eventual (comparar o ID da requisição), reconstrução com eventos arquivados e com snapshot. → [[CQRS]]

> [!question]- Carga full × carga delta?
> Full: reconstrução completa a partir de outros serviços. Delta: só as mudanças recentes. Num serviço novo: normalmente uma única full e depois as delta.

> [!question]- O que é o Saga, e quais as formas de coordenação?
> Transações distribuídas como uma sequência de transações locais, com transações de reversão em caso de falha; coreografia (cooperativa, por eventos) ou orquestração (centralizada). → [[Saga]]

## Dúvidas em aberto
- Aula 1: "diminuir o time-to-market" é ruim no monolito, mas "reduzir o time-to-market" é benefício dos microsserviços.
- Aula 4: o PDF padroniza o 401 para todos os cenários de controle de acesso, mas recomenda 404 para endpoints restritos.
- Aula 4: na tabela de respostas, o 403 Forbidden aparece como alternativa ao 401; na seção de segurança, a recomendação é padronizar o 401.

## Pontos fracos (o que errei)
