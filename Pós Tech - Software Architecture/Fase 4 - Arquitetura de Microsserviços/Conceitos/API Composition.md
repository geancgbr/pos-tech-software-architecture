---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [API Composer]
---

# API Composition

Padrão que faz **várias chamadas a várias APIs**, **agrega** os dados e envia ao cliente.

- **Exemplo** ([[MS 03 - Gerenciando API com API Gateway e BFF]]): a tela de produto do App precisa de descrição, preço e estoque; um endpoint no API Gateway chama **Catálogo de Produtos**, **Estoque** e **Precificação** e devolve **um único JSON**.
- **Latência** ([[MS 05 - Implementando queries com microsserviços]]): **paralelizar** as chamadas; o **API Composer** agrega conforme as respostas chegam.
- **Preferência**: pela facilidade, normalmente se prefere o API Composition; se os desafios o inviabilizarem, usar o [[CQRS]].
- **No Hands On da aula 5**: o serviço **Busca Produto**, endpoint "Obter Produto".

Aparece em: [[MS 03 - Gerenciando API com API Gateway e BFF]], [[MS 05 - Implementando queries com microsserviços]]
