---
tags: [pos-tech/fase-4, banco-de-dados, nosql, cache, conceito]
aliases: [Remote Dictionary Server, Banco de chave-valor, Bancos de chave-valor, Chave-valor]
---

# Redis

Banco **de chave-valor de código aberto**, conhecido pela **alta performance**; o nome abrevia **"Remote Dictionary Server"** ([[DE 03 - Bancos de chave-valor com Redis]]).

- **Tipos de valor**: strings · listas · conjuntos · **sorted sets** (com score) · **hashes**; e também HyperLogLogs, Bitmaps e Streams.
- **Recursos**: milhões de operações por segundo · **pub/sub** · **scripts Lua** atômicos · **persistência em disco** · **expiração automática de chaves** · clusters e replicação.
- **Usos**: **cache** (principalmente, mas não só), contadores em tempo real, filas de mensagens, sessões, análise em tempo real.
- **Custos**: o software é grátis, mas é preciso considerar a hospedagem própria (se optar por ela), os serviços gerenciados (**Amazon ElastiCache**, **Azure Cache for Redis**, **Google Cloud Memorystore**) e recursos adicionais.
- **Bancos de chave-valor em geral**: simples, rápidos por chave, escaláveis, flexíveis no valor, que **podem ter** limitações em consultas complexas. Primeiros sistemas: anos 1960 (ex.: **IMS**, IBM, 1966); pioneiro do conceito moderno: **Dynamo** (Amazon, 2004).

## Na Fase 1
Na [[ARQ 05 - Arquitetura Hexagonal]], uma porta de cache com adaptadores **Redis** e cache em memória ilustra as portas e adaptadores ([[Estratégias de Cache]]).

Aparece em: [[DE 01 - Fundamentação e SGBDs]], [[DE 03 - Bancos de chave-valor com Redis]]
