---
tags: [pos-tech/fase-4, microsservicos, saga, aula]
disciplina: SAGA Pattern
aula: 1
fonte: "SAGA Pattern/Aula 1 - Padrão SAGA - Introdução.pdf"
---

# SAGA 01 - Introdução ao padrão SAGA

[[SAGA Pattern]] · Próxima → [[SAGA 02 - Orquestração e coreografia]]

> [!summary] Em uma frase
> Operações como a **finalização de um pedido** num e-commerce envolvem várias tarefas que precisam acontecer de forma unificada. Nos anos 80, a tática mais comum era o **lock no banco**, que garantiam consistência mas **prejudicavam a velocidade**; em **1987**, **Hector Garcia-Molina e Kenneth Salem** propuseram o **padrão SAGA**: uma **sequência de transações locais coordenadas por mensagens**, com **transações compensatórias** em caso de falha. A SAGA oferece controle **ACD, e não ACID**. Ver [[Saga]].

## Hands On (vídeos)
Nas primeiras videoaulas: dilemas comuns em soluções de microsserviços, que **datam de décadas atrás**, quando o padrão era o desenvolvimento voltado para o **banco de dados**.

## O problema
- Exemplo: comprar algo num e-commerce como a **Amazon**; ao finalizar o pedido, uma série de operações é executada até a entrega (Figura 1, fluxo simplificado).
- **Uma possível estratégia** (Figura 2): executar em sequência "Criar Pedido", "Reservar Item Estoque" e "Gerar Boleto Cobrança" **na mesma transação**; com sucesso, a operação menos crítica, "Notificar cliente por e-mail", **poderia** ser executada; com insucesso, **nenhuma** operação deveria ser executada.
- Num **fluxo complexo** (Figura 3): o que fazer se ocorrer um erro depois de "Criar Pedido"?
  - O **padrão Retry** define novas tentativas e intervalos, mas e se o problema for **de negócio**? Ex.: o **cartão do cliente foi cancelado**; a **transportadora não pode entregar**.
- "Problemas podem acontecer e eles acontecerão." O tema **não é exclusivo de microsserviços**: nos **anos 80**, já se discutia como otimizar operações de banco compostas de várias **subtransações**.

## Locks no banco e a origem da SAGA
- Naquela época, a consistência transacional ficava **na camada do banco**; a tática mais comum era fazer **lock dos objetos** até a transação terminar. Garantia consistência, mas **prejudicava consideravelmente a velocidade**.
- No diagrama de atividades (Figura 4), a requisição do **componente 2** precisa **aguardar** a transação do **componente 1** terminar; em sistemas de larga escala, essa espera **pode** gerar grandes impactos para o negócio.
- Em **1987**, **Hector Garcia-Molina** e **Kenneth Salem** publicaram um paper com o **padrão SAGA**.

## O que é o padrão SAGA
- Com os microsserviços, a gestão de transações ficou **ainda mais desafiadora**. Em **cada** microsserviço ainda é possível uma transação local **ACID**; quando a operação envolve **vários**, é preciso uma estratégia auxiliar. Ver [[ACID]].
- Uma **SAGA** é uma **sequência de transações locais coordenadas através de mensagens**. Cada serviço é um **participante** e garante localmente transações ACID (Figura 5):

| Transação | Serviço | Operação | Operação compensatória (Figura 6) |
|---|---|---|---|
| 1 | Pedido | Criar pedido | — |
| 2 | Estoque | Reservar item estoque | **Cancelar reserva** |
| 3 | Cobrança | Efetuar cobrança via gateway | — |
| 4 | Cobrança | Criar registro contábil | **Criar registro reverso** |
| 5 | Notificação | Notificar cliente | — |
| 6 | Nota Fiscal | Gerar nota fiscal | — |
| 7 | Pedido | Atualizar pedido | — |

## Transações compensatórias
- Se a **cobrança** falhar, a SAGA é **interrompida** e a ação compensatória "Cancelar Reserva Estoque" é acionada. Por isso, a SAGA oferece um controle transacional **ACD, e não ACID**. Ver [[Transações Compensatórias]].
> [!note] A compensação se chama "Cancelar reserva" na tabela e "Cancelar Reserva Estoque" no texto.

- Em caso de falha, **de acordo com o impacto para o negócio**, devem ser previstas operações compensatórias que **revertam** as operações já executadas até o ponto do problema.
- Assim como se mapeia o **fluxo feliz** no design do domínio, é preciso mapear as **ações compensatórias viáveis para o negócio**.
- **Exemplo (seguros)**: dependendo do estágio da falha na SAGA de emissão de uma **apólice**, não dá para simplesmente cancelá-la; é preciso emitir um **endosso de cancelamento**.

## Para saber mais
**Pt. 1 – ACID**
| Propriedade | Definição do PDF |
|---|---|
| **Atomicidade** | Conjunto **indivisível** de operações: ou todas são executadas, ou nenhuma |
| **Consistência** | Leva os dados de um estado **válido** para outro estado válido |
| **Isolamento** | Técnicas que tentam evitar que transações paralelas sobre os mesmos dados **interfiram** umas nas outras; o resultado em paralelo é o mesmo de executá-las **uma após a outra** |
| **Durabilidade** | Transações **commitadas** continuam persistentes mesmo com falha do banco ou falta de energia |

**Pt. 2 – XA (Extended Architecture)**
- Nos **anos 90**, a **X/Open** publicou o **XA**, padrão para transações distribuídas que delegava a gestão a um **Transaction Manager**. Vários SGBDs (**mas não todos**) o adotaram, como **Oracle** e **MySQL**. Ver [[XA (Extended Architecture)]].
- Problemas: **locks distribuídos** entre as bases durante a transação; se o Transaction Manager ficasse **indisponível**, os locks eram mantidos até sua recuperação; em casos críticos, eram necessárias **intervenções manuais**.

## Referências
Richardson, *Microservices Patterns* (Manning, 2018) · Universidade Cornell: Sagas (2002) · Sofwancoder: Two-Phased Commit and eXtended Architecture
