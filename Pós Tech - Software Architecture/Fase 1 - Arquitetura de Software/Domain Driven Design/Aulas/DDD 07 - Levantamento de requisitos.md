---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 7
fonte: "Aula 07- Levantamento de requisitos.pdf"
---

# DDD 07 - Levantamento de requisitos

← [[DDD 06 - Event Storming]] · [[Domain Driven Design]] · Próxima → [[DDD 08 - Refinamento técnico]]

> [!summary] Em uma frase
> O levantamento de requisitos é a primeira etapa para transformar demanda de negócio em requisito de desenvolvimento. Ele reduz os [[Riscos de Produto (Marty Cagan)|riscos]], principalmente o técnico, e exige que o dev participe do [[Upstream e Downstream|upstream]].

## Os 4 riscos de Marty Cagan
| Risco | Pergunta | Quem valida e como |
|---|---|---|
| **Valor** (o mais sensível, avaliado primeiro) | O cliente precisa disso a ponto de pagar ou de se adaptar? | PM ou PO |
| **Negócio** | Agrega à estratégia? É viável financeiramente? Traz risco legal? | A apostila não especifica |
| **Usabilidade** | As pessoas vão conseguir usar? | Testes de usabilidade |
| **Técnico** (o foco do curso) | O time tem recursos técnicos, financeiros e humanos para construir? | Levantamento de requisitos e [[Refinamento Técnico]] |

## Upstream e downstream
- **Upstream**: do backlog de ideias à priorização, ao levantamento de requisitos e à transformação em tarefas. É onde se mapeia, explora e valida.
- **Downstream**: do início do desenvolvimento até o deploy, a "produção".
- Se o dev ou tech lead não participa do upstream, os problemas aparecem: **requisito mal compreendido**, **imprevisibilidade**, **bugs e débito técnico**.

## O que o documento da demanda precisa ter
1. **Persona**: quem vai usar a solução.
2. **Problema e jornada atual**: como a persona faz hoje e onde ela sofre.
3. **Objetivo**: a expectativa do negócio. Com ele claro, fica mais fácil definir o "como".
4. **Jornada da solução**: as etapas que a persona vai percorrer com a solução.
5. **[[Requisitos Funcionais e Não Funcionais]]**.

Se o documento não trouxer essas respostas, **vá atrás delas**: elas são a base das próximas etapas.

## Exemplo da aula: CRM integrado
- **Persona**: diretoria, gerência e analistas de vendas, além do cliente que pede proposta.
- **Hoje**: Excel. Há perda de informação, follow-up difícil e nenhum controle gerencial do pipeline. O pedido chega por e-mail, incompleto. O analista preenche o Excel em duas abas, monta um PowerPoint e envia por e-mail. Leva **3 dias úteis**, e o cliente cobra retorno no meio do caminho.
- **Objetivo**: centralizar as cotações numa plataforma, com metas de **+10% em vendas** e **−50% no tempo de resposta**.
- **RF**: cadastro de empresas e de cotações, follow-up automático, geração e envio automáticos da proposta, tracking do e-mail.
- **RNF**: segurança robusta, **99% de disponibilidade**, **100 usuários internos**, **1000 propostas simultâneas**, bom desempenho com grandes volumes.
