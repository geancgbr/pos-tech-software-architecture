---
tags: [pos-tech/fase-4, microsservicos, saga, revisao]
disciplina: SAGA Pattern
---

# Revisão - SAGA Pattern

[[SAGA Pattern]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- Por que o Retry não basta numa finalização de pedido?
> Porque o problema pode ser de negócio (ex.: cartão cancelado, transportadora sem poder entregar).

> [!question]- Qual era a tática mais comum nos anos 80, e qual o problema?
> O lock dos objetos no banco até o fim da transação; garantia consistência, mas prejudicava consideravelmente a velocidade.

> [!question]- Quem propôs o padrão SAGA, e quando?
> Hector Garcia-Molina e Kenneth Salem, em 1987.

> [!question]- O que é uma SAGA?
> Uma sequência de transações locais coordenadas através de mensagens; cada serviço é um participante que garante transações ACID locais. → [[Saga]]

> [!question]- Por que se diz que a SAGA oferece controle ACD, e não ACID?
> Porque falta o isolamento (o "I"), como mostra o exemplo da aula: em falha, a SAGA é interrompida e são acionadas operações compensatórias, previstas de acordo com o impacto para o negócio. A falta do "I" é o tema da aula 3. → [[Transações Compensatórias]]

> [!question]- Dê exemplos de operações compensatórias.
> Reservar item estoque → cancelar reserva; criar registro contábil → criar registro reverso; em seguros, emitir um endosso de cancelamento em vez de cancelar a apólice.

> [!question]- Defina as quatro propriedades ACID.
> Atomicidade (todas ou nenhuma), Consistência (de um estado válido para outro), Isolamento (técnicas que tentam evitar que transações paralelas interfiram) e Durabilidade (o que foi commitado persiste). → [[ACID]]

> [!question]- O que era o XA, e quais seus problemas?
> Especificação da X/Open (anos 90) que delegava as transações distribuídas a um Transaction Manager. Problemas: locks distribuídos e locks mantidos se o Transaction Manager caísse, às vezes com intervenção manual. → [[XA (Extended Architecture)]]

## Aula 2 - Orquestração e coreografia
> [!question]- Coreografia × orquestração: quem decide?
> Na coreografia, a decisão é distribuída entre os participantes, que trocam eventos (uma dança). Na orquestração, um orquestrador envia comandos (um maestro).

> [!question]- Prós e contras da coreografia?
> Prós: simplicidade e acoplamento fraco. Contras: mais difícil de entender, dependências cíclicas (podendo causar recursão infinita) e risco de forte acoplamento.

> [!question]- Prós e contras da orquestração?
> Prós: dependências simplificadas (mão única), acoplamento fraco e lógica centralizada. Contras: orquestrador complexo e ponto único de falha.

> [!question]- Segundo Chris Richardson, quando usar cada uma?
> Coreografia para SAGAs simples; nos demais cenários, a orquestração tende a ser mais benéfica.

> [!question]- Como a AWS implementa a SAGA na aula?
> Com AWS Step Functions: cada etapa (ex.: ProcessPayment) tem etapas separadas para sucesso (UpdateCustomerAccount) e falha (SetOrderFailure).

## Aula 3 - Falta do "I"
> [!question]- O que são Lost Updates?
> Uma SAGA sobrescreve, sem ler, as alterações feitas por outra. Impacto: o cliente recebe um pedido que deveria ter sido cancelado. → [[Anomalias de Dados em Sagas]]

> [!question]- O que são Dirty Reads?
> Uma transação ou SAGA lê atualizações de outra que ainda não terminou. Impacto: o cliente usou mais pontos do que tinha.

> [!question]- Como funciona a Pessimistic View?
> Reordena os passos para que os dados só sejam lidos depois de atualizados por todas as SAGAs (ex.: restituir os pontos só depois de cancelar a entrega). Pode aumentar a complexidade e reduzir o desempenho.

> [!question]- Como funciona o Reread Value?
> Relê os dados antes de atualizá-los; se mudaram desde a primeira leitura, a SAGA aborta a operação.

> [!question]- Quais os quatro níveis de isolamento, e qual o padrão do InnoDB?
> READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ (padrão do InnoDB) e SERIALIZABLE. → [[Níveis de Isolamento de Transações]]

## Aulas 4 e 5 - Na prática
> [!question]- Quais os serviços e tecnologias do projeto de referência?
> fiapstore-pedido, cobranca e entrega-service; Java, Spring Boot, Maven, H2 e arquitetura hexagonal.

> [!question]- Para que serve o `AUTO_SERVER=TRUE` no H2?
> Permite múltiplas conexões ao banco, possibilitando executar queries durante o serviço.

> [!question]- Para que servem as portas 5672 e 15672 do RabbitMQ?
> 5672: integração com os serviços; 15672: console web administrativo (guest/guest). → [[RabbitMQ]]

> [!question]- Na SAGA coreografada, que serviço a inicia, e o que acontece ao chegar mensagem em `entregas_confirmadas`?
> O fiapstore-pedido-service. A mensagem indica pagamento e entrega confirmados, e o caso de uso ConfirmarPedido muda o status para CONFIRMADO.

> [!question]- Por que salvar o pedido e publicar na fila ficam sob `@Transactional`?
> Porque as duas operações precisam ser atômicas: "ALL or NONE".

> [!question]- Como a SAGA orquestrada é implementada?
> Com o Apache Camel: a classe SagaPedido define rotas sobre filas `orquestracao_*` do exchange `demo` e recebe as respostas em `orquestracao_pedidos_saga_reply`. → [[Apache Camel]]

> [!question]- Qual a vantagem e o risco da versão orquestrada, segundo a conclusão?
> É mais fácil de entender, porque tudo está num único ponto; mas a indisponibilidade do serviço de pedidos poderia parar todo o processamento.

## Pontos fracos
- 
