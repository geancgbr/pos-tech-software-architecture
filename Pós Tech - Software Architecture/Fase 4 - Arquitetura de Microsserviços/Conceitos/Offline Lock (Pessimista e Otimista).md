---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Pessimistic Offline Lock, Optimistic Offline Lock, Bloqueio pessimista, Bloqueio otimista]
---

# Offline Lock (Pessimista e Otimista)

Padrões para **transações de negócio concorrentes** ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]).

| | Pessimistic Offline Lock | Optimistic Offline Lock |
|---|---|---|
| Ideia | **Uma transação por vez**: adquire um **bloqueio** antes de usar o dado | Antes do **commit**, verifica se o dado **mudou**; havendo conflito, **reverte**. Supõe conflitos **raros** |
| Exemplo | **Sistema bancário**: a conta fica bloqueada durante a transferência | **Reserva de assentos**: todos tentam; no commit, verifica-se se o assento ainda está livre |
| Vantagens | Evita conflitos · previsibilidade | **Alta concorrência** · desempenho |
| Desvantagens | Baixa concorrência · esperas mais longas | Conflitos e retrabalho em alta competição · complexidade (padrões como **Aggregate**) · frustração do usuário |

- No Hands On, o padrão **Aggregate** **pode auxiliar** a lidar com a concorrência ao alterar preços de vários produtos ao mesmo tempo; segundo o resumo, as alterações são versionadas pela entidade principal ([[Agregado]]).

Aparece em: [[MS2 02 - Aplicando a lógica de negócios no microsserviço]]
