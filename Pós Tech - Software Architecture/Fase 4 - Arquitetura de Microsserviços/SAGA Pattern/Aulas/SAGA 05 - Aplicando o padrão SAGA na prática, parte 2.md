---
tags: [pos-tech/fase-4, microsservicos, saga, aula]
disciplina: SAGA Pattern
aula: 5
fonte: "SAGA Pattern/Aula 5 - Aplicando o padrão SAGA na prática - Parte II.pdf"
---

# SAGA 05 - Aplicando o padrão SAGA na prática, parte 2

← [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]] · [[SAGA Pattern]]

> [!summary] Em uma frase
> Implementa as duas modalidades no projeto de referência: a **coreografada**, com filas do **RabbitMQ** e as classes de comunicação `PedidoQueueAdapterIN/OUT` no `fiapstore-pedido-service`, que **inicia** a SAGA; e a **orquestrada**, com o **Apache Camel** e a classe `SagaPedido`, que envia comandos e recebe as respostas em `orquestracao_pedidos_saga_reply`. A orquestrada é **mais fácil de entender**, mas a indisponibilidade do serviço de pedidos **poderia parar** todo o processamento.

## Hands On
Implementar, na prática, as duas estratégias de SAGA e observar particularidades apresentadas nas aulas teóricas.

## SAGA coreografada
- Até aqui, os serviços são **ilhas isoladas**, com transações só locais. Diagrama da implementação: Figura 1.
- **Subir o RabbitMQ** (material de apoio no GitHub da disciplina; Figura 2) e acessar o painel com **guest** (Figura 3). Ver [[RabbitMQ]].
```bash
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.12-management
```
- **Criar as filas** (campo NAME + botão **ADD QUEUE**; Figura 4): `pedidos`, `entregas_confirmadas`, `pagamentos_confirmados`, `pagamentos_pendentes`.
- **Registrar** as filas e a conexão com o RabbitMQ no `application.yml`: **só em imagem**, ver as Figuras 5 e 6 do PDF (a legenda da Figura 6 escreve "applcation.yml").
- **Dependência** no `pom.xml` (mostrada no pedido-service; vale para os outros):
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```
- **Interfaces** em `domain/repository` (Figura 7):
```java
package br.com.fiapstore.pedido.domain.repository;

import br.com.fiapstore.pedido.domain.exception.OperacaoInvalidaException;
import br.com.fiapstore.pedido.domain.exception.PedidoNaoEncontradoException;
import br.com.fiapstore.pedido.domain.exception.PercentualDescontoAcimaDoLimiteException;
import org.springframework.messaging.handler.annotation.Payload;

public interface IPedidoQueueAdapterIN {
    void receive(@Payload String message) throws PedidoNaoEncontradoException,
            PercentualDescontoAcimaDoLimiteException, OperacaoInvalidaException;
}
```
```java
package br.com.fiapstore.pedido.domain.repository;

public interface IPedidoQueueAdapterOUT {
    void publish(String message);
}
```
- O `fiapstore-pedido-service` **inicia a SAGA**: posta mensagens quando recebe uma requisição de criação de pedido e **escuta** mensagens dos outros serviços (classes de comunicação: Figura 8).

> [!note] A extração perdeu a indentação e quebrou nomes longos nos códigos desta aula; eles foram remontados. O PDF escreve o pacote como "domain/repositor".

### Postagem de mensagens
Toda requisição de novo pedido é **salva localmente** e **publicada na fila**:
```java
@Service
public class PedidoQueueAdapterOUT implements IPedidoQueueAdapterOUT {

    private final Logger logger = LoggerFactory.getLogger(this.getClass());

    @Autowired
    private RabbitTemplate rabbitTemplate;

    @Value("${queue1.name}")
    private String pedidosPendentes;

    @Override
    public void publish(String message) {
        rabbitTemplate.convertAndSend(pedidosPendentes, message);
        logger.info("Publicação na fila pedidos executada");
    }
}
```
- No caso de uso `RegistrarPedido.java` (Figura 9), a **linha 53** passa a publicar na fila. As duas operações precisam ser **atômicas** ("ALL or NONE", como diz a música do **Pearl Jam**): por isso ficam na **mesma transação** com `@Transactional`, na **linha 39**.

### Escuta de mensagens
```java
@Service
public class PedidoQueueAdapterIN implements IPedidoQueueAdapterIN {

    private final Logger logger = LoggerFactory.getLogger(this.getClass());

    @Autowired
    private Gson gson;

    private final ConfirmarPedidoUseCase confirmarPedidoUseCase;

    @Autowired
    public PedidoQueueAdapterIN(ConfirmarPedidoUseCase confirmarPedidoUseCase) {
        this.confirmarPedidoUseCase = confirmarPedidoUseCase;
    }

    @RabbitListener(queues = {"${queue4.name}"})
    public void receive(@Payload String message) throws PedidoNaoEncontradoException,
            PercentualDescontoAcimaDoLimiteException, OperacaoInvalidaException {
        HashMap<String, String> mensagem = gson.fromJson(message, HashMap.class);
        confirmarPedidoUseCase.executar(mensagem.get("codigoPedido"));
        logger.info("Confirmação de pedido registrado");
    }
}
```
- Monitora a fila **`entregas_confirmadas`**: uma mensagem nela significa que o pedido já teve **pagamento e entrega confirmados**; em resposta, o caso de uso **ConfirmarPedido** atualiza o status para **CONFIRMADO**.

### Testando
Fazer requisições ao endpoint de criação de pedidos (Figura 10); as mensagens devem aparecer na fila **pedidos** (Figura 11). Depois, repetir os passos para os serviços de **cobrança** e **entrega**; o código está no repositório oficial, branch **`coreografia`**.

## SAGA orquestrada
- Vantagem: concentra a maior parte da lógica de integração **num único ponto**. Contra: a indisponibilidade desse ponto **interrompe toda a operação**. Diagrama: Figura 12.
- **Dependências** do Apache Camel no `pom.xml`. Ver [[Apache Camel]].
```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>4.1.0</version>
</dependency>
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-rabbitmq-starter</artifactId>
    <version>4.1.0</version>
</dependency>
```
- **Novas filas**: `orquestracao_pagamentos`, `orquestracao_entregas`, `orquestracao_pedidos`, `orquestracao_pedidos_saga_reply`. Antes, criar um **exchange** chamado **`demo`** (Figura 13); as filas criadas aparecem na Figura 14.
- **Classe `SagaPedido`** (Figura 15), que define a estratégia de orquestração. Ela envia **comandos** aos outros serviços, que respondem pela fila `orquestracao_pedidos_saga_reply`:
```java
@Override
public void configure() throws Exception {
    from("spring-rabbitmq:demo?queues=orquestracao_pedidos&routingKey=orquestracao_pedidos&arg.queue.durable=true")
        .log(LoggingLevel.WARN, "Novo Pedido Recebido")
        .bean(MensagemFila.class, "fromJsonToMap(${body})")
        .convertBodyTo(String.class)
        .to("spring-rabbitmq:demo?queues=orquestracao_pagamentos&routingKey=orquestracao_pagamentos&arg.queue.durable=true");

    from("spring-rabbitmq:demo?queues=orquestracao_pedidos_saga_reply&routingKey=orquestracao_pedidos_saga_reply&arg.queue.durable=true")
        .routeId("Rota orquestracao_pedidos_saga_reply")
        .log(LoggingLevel.WARN, "${body}")
        .choice()
            .when(body().contains("atualizacaoPagamento"))
                .to("spring-rabbitmq:demo?queues=orquestracao_entregas&routingKey=orquestracao_entregas&arg.queue.durable=true")
            .when(body().contains("\"statusEntrega\":\"CONFIRMADA\""))
                .log(LoggingLevel.WARN, "entrega confirmada")
                .bean(SagaPedido.class, "confirmarPedido(${body})")
                .log(LoggingLevel.WARN, "Pedido confirmado");
}

public void confirmarPedido(String json) throws PedidoNaoEncontradoException,
        PercentualDescontoAcimaDoLimiteException, OperacaoInvalidaException {
    HashMap<String, String> map = MensagemFila.fromJsonToMap(json);
    confirmarPedidoUseCase.executar(map.get("codigoPedido"));
}
```
- Comportamento resultante: Figura 16. Depois, configurar de forma semelhante os demais serviços.

> [!warning] Inconsistências do PDF
> - O texto diz que os pedidos são postados em "ORQUESTRACAO_PEDIDO" e, depois do processamento, em "ORQUESTRAÇÃO_ENTREGA"; o código manda de `orquestracao_pedidos` para **`orquestracao_pagamentos`**, e só a resposta com `atualizacaoPagamento` segue para `orquestracao_entregas`.
> - A lista de filas escreve "**O**rquestracao_entregas", com maiúscula; o código usa `orquestracao_entregas`.

## Conclusão
- "É notório" o quanto a SAGA **orquestrada** é **mais fácil de entender**, porque tudo está num **único ponto**; por outro lado, a indisponibilidade do **serviço de pedidos**, onde a SAGA está definida, **poderia parar** todo o processamento.

## Para saber mais
- Implementar SAGAs é **muito complexo**: os possíveis fluxos devem ser exercitados, refeitos e **validados pelo público envolvido** na etapa de design.
- Ferramentas como **DRAWIO, EXCALIDRAW ou LUCIDCHAR** (grafia do PDF) são fundamentais para mostrar visualmente o comportamento planejado; **versionar e manter** essa documentação é tarefa do time.

## Referências
Apache Camel User Manual · RabbitMQ: página oficial · Richardson, *Microservices Patterns*
