---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Nível de isolamento, READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE]
---

# Níveis de Isolamento de Transações

Determinam como transações concorrentes **veem as alterações** de outras; mais alto = **mais consistência**, mas **pode** reduzir o desempenho. É comum os bancos oferecerem a possibilidade de configurá-lo para balancear com a performance ([[SAGA 03 - Lidando com a falta do I do ACID]]).

| Nível | O que o PDF diz |
|---|---|
| **READ UNCOMMITTED** | O mais baixo: **permite** ler dados de transações **não confirmadas** |
| **READ COMMITTED** | **Permite** ler dados modificados e **confirmados** |
| **REPEATABLE READ** | Impede ler dados não confirmados e garante ver **os mesmos dados duas vezes**, mesmo se outras transações os modificarem entre as leituras; é o **padrão do InnoDB** (MySQL) |
| **SERIALIZABLE** | O mais alto: como se as transações fossem **uma de cada vez** |

- O **InnoDB** oferece os quatro níveis do padrão **SQL:1992**.

Aparece em: [[SAGA 03 - Lidando com a falta do I do ACID]]
