---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [Transações ACID, Atomicidade, Consistência, Isolamento, Durabilidade]
---

# ACID

Propriedades de uma transação ([[SAGA 01 - Introdução ao padrão SAGA]]):

| Propriedade | Definição do PDF |
|---|---|
| **Atomicidade** | Conjunto **indivisível** de operações: todas ou nenhuma |
| **Consistência** | Leva os dados de um estado **válido** para outro válido |
| **Isolamento** | Técnicas que **tentam evitar** que transações paralelas sobre os mesmos dados **interfiram** umas nas outras; resultado igual ao de executá-las uma após a outra |
| **Durabilidade** | Transações **commitadas** persistem mesmo com falha do banco ou falta de energia |

- Em **cada** microsserviço, ainda é possível uma transação local ACID; entre vários, é preciso uma estratégia como a [[Saga]], que oferece controle **ACD, e não ACID** ([[SAGA 01 - Introdução ao padrão SAGA]]).
- A falta do **"I"** **pode** gerar [[Anomalias de Dados em Sagas]]; os bancos permitem configurar o [[Níveis de Isolamento de Transações|nível de isolamento]] ([[SAGA 03 - Lidando com a falta do I do ACID]]).
- No projeto de referência (aula 5), salvar o pedido e publicá-lo na fila devem ser **atômicos** ("ALL or NONE"), com `@Transactional` ([[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]).

Aparece em: [[SAGA 01 - Introdução ao padrão SAGA]], [[SAGA 03 - Lidando com a falta do I do ACID]], [[SAGA 05 - Aplicando o padrão SAGA na prática, parte 2]]
