---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Idempotency, Idempotency Key, Chave de idempotência]
---

# Idempotência

Uma operação **idempotente** pode ser executada **várias vezes seguidas** com o **mesmo resultado**, sem duplicidade ou inconsistência ([[RES 02 - Padrões de resiliência]]).

- **Chave de idempotência**: informação única que identifica uma requisição, comando ou intenção; enviada **nos cabeçalhos HTTP ou como parâmetro**; **pode** ser gerada pelo cliente ou a partir de dados da requisição ([[RES 02 - Padrões de resiliência]]).
- **Três etapas** ([[RES 03 - Resiliência na prática]]): gerar a **Idempotency Key** (**geralmente** pelo cliente, ex.: **UUID**, no cabeçalho) → **armazenar** chave + resposta num repositório persistente → numa repetição, **retornar a resposta armazenada**.
- Recomendações: **expiração** das chaves (ex.: 24 h) e **banco transacional** contra condições de corrida ([[RES 03 - Resiliência na prática]]).
- É **essencial** para usar [[Retry e Backoff Exponencial|retries]] ([[RES 02 - Padrões de resiliência]]) e uma das boas práticas do Retry Pattern ([[RES 04 - Service Mesh e controle de tráfego]]).
- Exemplo do PDF: **API de pagamentos**, em que a cobrança acontece **uma só vez**.

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]], [[RES 04 - Service Mesh e controle de tráfego]]
