---
tags: [pos-tech/fase-4, microsservicos, saga, aula]
disciplina: SAGA Pattern
aula: 3
fonte: "SAGA Pattern/Aula 3 - Lidando com a falta do “I” do ACID.pdf"
---

# SAGA 03 - Lidando com a falta do "I" do ACID

← [[SAGA 02 - Orquestração e coreografia]] · [[SAGA Pattern]] · Próxima → [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]

> [!summary] Em uma frase
> Sem o **isolamento**, SAGAs concorrentes **podem** sofrer **anomalias de dados**: **Lost Updates** (uma SAGA sobrescreve, sem ler, o que outra alterou) e **Dirty Reads** (uma SAGA lê atualizações de outra ainda incompleta). Duas das contramedidas vistas são a **Pessimistic View** (reordenar os passos) e o **Reread Value** (reler antes de atualizar e abortar se mudou). É comum os bancos permitirem configurar o **nível de isolamento** para balancear com a performance. Ver [[Anomalias de Dados em Sagas]].

## Hands On
Nesta sequência de aulas: questões importantes ao trabalhar com SAGAs, **problemas comuns** e **contramedidas** para mitigar riscos.

## Anomalias de dados
### Lost Updates (atualizações perdidas)
- Na Figura 1, a **SAGA 2** realiza uma operação sobre o **pedido 100** antes de a **SAGA 1** ser concluída.
- **Definição**: uma SAGA **sobrescreve, sem ler**, as alterações feitas por outra SAGA.
- **Impacto no e-commerce**: a pessoa cliente recebe um pedido que **deveria ter sido cancelado**.

### Dirty Reads (leituras sujas)
Contexto: um **programa de pontos** com que os clientes pagam produtos. Compra paga com pontos seguida de cancelamento:

| SAGA | Operação | Valor | Saldo |
|---|---|---|---|
| | Saldo inicial | | 100 |
| Fazer pedido | Fazer pagamento | −100 | 0 |
| Fazer pedido | Agendar entrega | | 0 |
| Cancelar pedido | Cancelar pagamento | 100 | 100 |
| Cancelar pedido | Cancelar entrega | | |
| | **Saldo final** | | **100** |

Situação hipotética com as mesmas SAGAs **intercaladas**:

| SAGA | Operação | Valor | Saldo |
|---|---|---|---|
| | Saldo inicial | | 0 |
| Cancelar pedido | Cancelar pagamento | 100 | 100 |
| Fazer pedido | Fazer pagamento | −100 | 0 |
| Cancelar pedido | Cancelar entrega | | |
| Fazer pedido | Agendar entrega | | 0 |
| Cancelar pedido | Operação compensatória devido à impossibilidade de cancelar | −100 | −100 |
| | **Saldo final** | | **−100** |

- No segundo cenário, o saldo fica **inconsistente**.
- **Definição**: uma transação ou SAGA **lê as atualizações** feitas por uma SAGA que **ainda não as completou**.
- **Impacto**: o cliente usou **mais pontos do que possuía**.

## Contramedidas
| Contramedida | Como funciona | Exemplo do PDF |
|---|---|---|
| **Pessimistic View** (visão pessimista) | **Reordena os passos** da SAGA para que os dados sejam lidos **somente depois** de atualizados por todas as SAGAs que precisam atualizá-los. **Pode** ser eficaz contra **Dirty Reads**, mas **pode** aumentar a complexidade e reduzir o desempenho | A restituição dos pontos ocorre **só depois do cancelamento da entrega** (tabela abaixo) |
| **Reread Value** (reler valor) | **Relê os dados** que a SAGA vai atualizar **antes** de atualizá-los; se mudaram desde a primeira leitura, a SAGA **aborta** a operação. **Pode** ser usada para evitar **Lost Updates** | No caso do pedido 100, a SAGA poderia **reler o status** antes de atualizá-lo para **aprovado** (Figura 2, operação de aprovação abortada) |

Versão reordenada (Pessimistic View):

| SAGA | Operação | Valor | Saldo |
|---|---|---|---|
| | Saldo inicial | | 0 |
| Cancelar pedido | Cancelar entrega | | 0 |
| Cancelar pedido | Cancelar pagamento | 100 | 100 |
| Fazer pedido | Fazer pagamento | −100 | 0 |
| Fazer pedido | Agendar entrega | | 0 |
| | **Saldo final** | | **100** |

> [!warning] Inconsistências do PDF
> - Na tabela da Pessimistic View, a coluna de saldo termina em **0**, mas o saldo final informado é **100**.
> - A tabela intercalada diz trazer "as mesmas SAGAS", mas começa com saldo inicial **0**; a primeira começa com **100**. A da Pessimistic View também começa em 0.
> - No PDF, o exemplo de reler o status do pedido 100 está no parágrafo da **Pessimistic View**; pelo assunto (Lost Updates), a nota o colocou no Reread Value.
> - O "O que você viu" chama a segunda contramedida de "**Rever** Valor"; no corpo, ela é "**Reler** Valor" (Reread Value).

## Para saber mais: sobrevivendo sem o "I" do ACID
- Trabalhar sem isolamento parece inaceitável, mas é comum os bancos permitirem **configurar o nível de isolamento** para balancear com a **performance**. Ver [[Níveis de Isolamento de Transações]].
- Documentação do **MySQL**: o **InnoDB** oferece os quatro níveis do **SQL:1992**; o padrão do InnoDB é **REPEATABLE READ**.
- O nível de isolamento determina como transações concorrentes **veem as alterações** das outras; mais alto = **mais consistência**, mas **pode** reduzir o desempenho.

| Nível | O que o PDF diz |
|---|---|
| **READ UNCOMMITTED** | O mais **baixo**: **permite** ler dados modificados por transações **não confirmadas** |
| **READ COMMITTED** | **Permite** ler dados modificados e **confirmados** por outras transações |
| **REPEATABLE READ** | Impede ler dados de transações não confirmadas e garante ver **os mesmos dados duas vezes**, mesmo que outras os modifiquem entre as leituras |
| **SERIALIZABLE** | O mais **alto**: as transações executam como se fossem **uma de cada vez** |

## O que você viu
A ausência de isolamento **pode** gerar sérios problemas para a solução e o negócio, mas já existem **diversas contramedidas** mapeadas, como a "Visão Pessimista" e o "Rever Valor".

## Referências
Microsoft: Transações distribuídas do SAGA · MySQL: InnoDB transaction isolation levels · Richardson, *Microservices Patterns*

> [!note] Nas referências, o link da documentação do MySQL aparece com o título "Transações distribuídas do SAGA", o mesmo da referência da Microsoft.
