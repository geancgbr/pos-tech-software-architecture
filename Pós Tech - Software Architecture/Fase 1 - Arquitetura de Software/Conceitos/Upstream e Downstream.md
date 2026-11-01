---
tags: [pos-tech/fase-1, conceito]
aliases: [Upstream, Downstream]
---

# Upstream e Downstream

> [!warning] O curso usa esses termos com **dois sentidos diferentes**

## 1. Entre contextos (aula 4)
- **Upstream (U)**: o **fornecedor**, que provê o serviço.
- **Downstream (D)**: o **cliente**, que consome.
- Base dos [[Padrões de Integração entre Contextos]].

## 2. No fluxo de desenvolvimento (aula 7)
- **Upstream**: backlog, priorização, levantamento de requisitos, validação. É transformar ideia em tarefa.
- **Downstream**: do início do desenvolvimento até o deploy.
- O dev ou tech lead **precisa participar do upstream**. Se não participa, o resultado é requisito mal entendido, imprevisibilidade, bugs e débito técnico.

## Na disciplina Monitoramento e Acesso Avançado (Fase 3)
Nos mapas de serviço do New Relic, aparecem os serviços **dos quais o seu serviço depende (upstream)** e os que **dependem dele (downstream)** ([[MAV 12 - Contexto Map New Relic]]).

Aparece em: [[DDD 04 - Trabalhando com contextos delimitados]], [[DDD 07 - Levantamento de requisitos]], [[MAV 12 - Contexto Map New Relic]]
