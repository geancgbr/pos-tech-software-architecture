---
tags: [pos-tech/fase-4, resiliencia, microsservicos, aula]
disciplina: Resiliência em Microsserviços
aula: 2
fonte: "Resiliência em microservices/Aula 02 - Padrões de Resiliência.pdf"
---

# RES 02 - Padrões de resiliência

← [[RES 01 - Introdução à resiliência]] · [[Resiliência em Microsserviços]] · Próxima → [[RES 03 - Resiliência na prática]]

> [!summary] Em uma frase
> Os microsserviços trazem **latência** (múltiplos saltos na rede), dificuldade de **consistência** e **falhas em cascata**. A aula apresenta as técnicas de base (**idempotência, timeout e retry**, com retries **imediatos, assíncronos e com backoff exponencial**) e os padrões **Circuit Breaker, Bulkhead, Rate Limiting, Timeout, Graceful Degradation, Failover e Throttling**, com prós e contras. Os padrões costumam ser **combinados**.

## Hands On (vídeos)
Nas videoaulas: aprofundar os padrões de resiliência e analisar as estratégias mais adequadas para cada cenário, comparando **benefícios e limitações** em situações práticas.

## Desafios e referência
- Desafios: **latência** (múltiplos saltos na rede), **consistência** dos dados entre serviços e falhas em um único componente que **podem** desencadear **efeitos em cascata**.
- Michael T. Nygard, em *Release It!: Design and Deploy Production-Ready Software*, apresenta padrões como **Circuit Breaker** e **Bulkhead**.

> [!note] O texto atribui *Release It!* a **Michael T. Nygard**; nas referências do PDF, o livro aparece como "NORMAN, M.".

## Técnicas fundamentais
### Idempotência
- Uma operação **idempotente** pode ser executada **várias vezes seguidas**, sempre com o **mesmo resultado**, sem duplicidade ou inconsistência. Com isso, dá para **repetir a operação** diante de falhas de rede, quedas ou manutenção. Ver [[Idempotência]].
- **Normalmente** se escolhe uma informação única, a **chave de idempotência**, que identifica uma requisição, um comando ou uma intenção do domínio. O sistema verifica se a operação **já foi realizada**.
- **Exemplo (API de pagamentos)**: o cliente inclui a chave **nos cabeçalhos HTTP ou como parâmetro da requisição**; o servidor a **valida e registra antes de processar**. A chave **pode** ser gerada pelo cliente ou a partir de dados da requisição. Resultado: **uma só cobrança**, mesmo com reenvios.
- Ver as Figuras 2 (baeldung) e 3 (AWS) do PDF.

> [!note] A primeira figura da aula é a **Figura 2**; não há Figura 1.

### Timeout
- Um **"relógio de segurança"**: define um tempo limite e **interrompe** a operação (no cliente ou no servidor) quando ele é ultrapassado. Evita conexões abertas sem necessidade, sobrecarga e **falhas em cascata**; permite acionar **fallback**. Ver [[Timeout]].
- Na maioria das vezes, **pode** ser configurado com ajustes simples nas bibliotecas ou componentes já usados. Ver a Figura 4 do PDF (DZone, Setting Request Timeout).

> [!note] O Timeout aparece duas vezes na aula: como técnica fundamental e, depois, na lista de padrões.

| Tipo | O que controla |
|---|---|
| **Connection Timeout** | Tempo máximo para **criar a conexão** cliente-servidor; sem ele, o cliente **poderia** esperar para sempre, algo comum em conexões TCP com bancos sobrecarregados ou APIs lentas |
| **Read/Write Timeout** | Tempo para **ler ou enviar dados** depois da conexão estabelecida; útil quando o serviço responde muito devagar |
| **Idle Timeout** | **Fecha conexões paradas** sem uso por muito tempo, liberando recursos |

### Estratégias de retry
- Repetir uma requisição diante de **falha temporária** (rede, indisponibilidade momentânea). Simples e eficaz para **erros transitórios**, mas com cuidado: é **essencial** combinar com **idempotência**. Ver [[Retry e Backoff Exponencial]].

| Estratégia | Como funciona |
|---|---|
| **Retries imediatos em memória** | Em memória, **geralmente na mesma thread** da requisição original; o tipo mais simples, comum em clientes HTTP e bibliotecas REST. Ex.: a API de pagamentos retorna **HTTP 503**; o cliente repete até ter sucesso ou atingir o **número máximo de tentativas**, sem filas. Tentativas **excessivas** podem agravar a indisponibilidade (Figura 5) |
| **Retries assíncronos** | As operações não ficam presas a uma resposta imediata, o que **desacopla** sistemas. Ex.: a requisição começa síncrona e termina assíncrona: em vez de **201 Created**, o sistema **pode** responder **202 Accepted** (recebida, será processada em segundo plano). Quando possível, é uma alternativa de **fallback**: armazenar as requisições que falharam e completá-las depois |
| **Retries com backoff exponencial** | Em vez de intervalos fixos, o tempo de espera **aumenta progressivamente** (ex.: 1 s, 2 s, 4 s, 8 s, 16 s...). Dá tempo para o destino se recuperar e reduz o risco de sobrecarregá-lo (Figura 6) |

## Padrões de resiliência
| Padrão | O que faz | Exemplo do PDF | Prós | Contras |
|---|---|---|---|---|
| **Circuit Breaker** (Figura 7) | Inspirado no disjuntor elétrico: monitora as chamadas e **bloqueia** requisições com **alta taxa de erros**. Estados: **fechado** (fluxo normal), **aberto** (bloqueia por um tempo) e **meio aberto** (algumas requisições testam a recuperação). Implementações: **Resilience4j** ou **Hystrix**. Ver [[Circuit Breaker]] | Uma API externa começa a falhar: o circuito **abre** e interrompe as chamadas que provavelmente falhariam | Previne falhas em cascata · reduz a latência ao evitar tentativas inúteis · melhora a estabilidade | **Pode** ser complexo configurar os limites · requer monitoramento contínuo |
| **Bulkhead** (Figura 8) | Inspirado nos **compartimentos de um navio**: isola partes do sistema, alocando recursos (**threads, conexões**) a grupos de operações, para que uma falha não **esgote todos os recursos**. Útil com múltiplos clientes ou serviços; combina com o Circuit Breaker. Ver [[Bulkhead]] | E-commerce: threads para **pagamentos** e outras para **cadastro**; sobrecarga no cadastro não afeta as compras | Limita o impacto de falhas · facilita priorizar operações críticas | Planejamento detalhado · **pode** desperdiçar recursos subutilizados |
| **Rate Limiting** (Figura 9) | Controla **quantas requisições** são processadas por período; muito usado em **APIs públicas**. Estratégias como o **Token Bucket** (cada requisição consome um token; sem tokens, novas requisições são **negadas ou enfileiradas**). Ferramentas como **NGINX** ou **Redis** são **comumente** usadas. Garante experiências mais **justas** entre usuários. Ver [[Rate Limiting e Throttling]] | API pública com **100 requisições por minuto** por cliente; o excedente recebe erro | Protege contra **DDoS** · mantém os serviços sob alta demanda | **Pode** frustrar usuários legítimos em picos · requer políticas claras |
| **Timeout** | Limite de tempo para operações; libera recursos e evita **bloqueios em cascata**. Frameworks permitem configurá-lo em vários níveis (rede a API) | Timeout de **3 s** num serviço externo; busca de site de notícias que cancela acima de **2 s**, com resultado parcial ou erro | Libera recursos rapidamente · evita gargalos de serviços lentos | Ajustes precisos (nem curto nem longo demais) |
| **Graceful Degradation** | Continuar com as funcionalidades **essenciais** mesmo com partes degradadas, sob alta carga ou indisponíveis. É **preventivo**: ativado automática ou manualmente (muitas vezes com **feature toggles**), desativando temporariamente o secundário. O **fallback** age **depois** do problema. Ver [[Fallback e Graceful Degradation]] | — | — | — |
| **Failover** (Figura 10) | Redireciona **automaticamente** o tráfego para instâncias ou serviços **redundantes**; comum em balanceadores e clusters de banco. **AWS** e **Google Cloud** oferecem soluções integradas. Ver [[Failover]] | Um cluster de banco detecta a falha do **nó primário** e transfere para o **secundário** | — | — |
| **Throttling** | Ajusta **dinamicamente** a taxa permitida conforme a **carga**; mais adaptável que o Rate Limiting. Sob sobrecarga, reduz as requisições ou retorna **429 Too Many Requests**. **Frequentemente** usado junto com Rate Limiting | Streaming que reduz a qualidade do vídeo ou as conexões simultâneas em picos | Protege contra sobrecarga · mantém operações críticas | **Pode** degradar operações não críticas |

> [!note] A legenda da Figura 10 é "Failover **Figure 2**".

## Combinação dos padrões
- Sistemas distribuídos **frequentemente** combinam padrões. Ex.: **Rate Limiting** contra a sobrecarga inicial, **Circuit Breaker** protegendo os serviços internos e **Bulkhead** isolando recursos críticos.
- **Monitoramento contínuo** e ajustes finos permitem que os padrões trabalhem integrados.

## O que vem por aí
Implementar resiliência em **Java** com o **Resilience4j** (Circuit Breaker, Retry, Bulkhead).

## Referências
AWS: Circuit breaker (Prescriptive Guidance) · AWS: funções idempotentes do Lambda com Powertools · D'Souza (JSession4D): Resilience4j com Spring Boot · DZone: Handling service timeouts using Istio · Kleppmann, *Designing data-intensive applications* · Lydtech Consulting: Resilience4j · Natter (Microsoft Learn): Application resiliency patterns · Norman, *Release it!* · Resilience4j: Getting started
