---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Timeout Pattern, Tempo limite, Connection Timeout, Read/Write Timeout, Idle Timeout]
---

# Timeout

Um **"relógio de segurança"**: define um tempo limite e **interrompe** a operação quando ele é ultrapassado, evitando conexões presas, sobrecarga e **falhas em cascata** ([[RES 02 - Padrões de resiliência]]).

| Tipo ([[RES 02 - Padrões de resiliência]]) | O que controla |
|---|---|
| **Connection Timeout** | Tempo para **criar a conexão** |
| **Read/Write Timeout** | Tempo para **ler ou enviar dados** com a conexão aberta |
| **Idle Timeout** | Fecha conexões **paradas** |

- **Prós**: libera recursos e evita gargalos de serviços lentos. **Contras**: ajustes precisos ([[RES 02 - Padrões de resiliência]]).
- **Na prática** ([[RES 03 - Resiliência na prática]]): em Go, `context.WithTimeout` de 2 s e **504 Gateway Timeout**; ajustar ao tempo esperado de cada serviço, `defer cancel()` e **fallback** em operações críticas.
- **No Service Mesh** ([[RES 04 - Service Mesh e controle de tráfego]]): evita **bloqueio de recursos**, melhora a **responsividade** e ajuda a **identificar gargalos**; configuração **centralizada**.

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]], [[RES 04 - Service Mesh e controle de tráfego]]
