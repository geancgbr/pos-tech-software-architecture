---
tags: [pos-tech/fase-3, serverless, aws, conceito]
aliases: [Lambda, Lambdas, Função Lambda, Funções Lambda]
---

# AWS Lambda

Serviço de **computação serverless orientado a eventos** da AWS: executa código **sem provisionar ou gerenciar servidores**, em resposta a eventos. "Geralmente, quando pensamos em serverless, o AWS Lambda é a primeira resposta!"

- **Funções** pequenas, que normalmente têm **uma única responsabilidade**, em Node.js, Python, Java, C# e outras ([[SLS 06 - AWS Lambda e AWS SAM]]).
- Pode ser chamado a partir de **mais de 200 serviços AWS**; paga-se **só pelo que usar** ([[SLS 01 - Recursos serverless na AWS]]).
- **Quando usar**: rotinas, scripts rápidos, APIs menores (aula 1); APIs com **picos de uso** ou tarefas em **alguns horários** (aula 6).
- **Triggers**: API Gateway · AWS IoT · S3 · SNS e SQS. Ao terminar, pode ter um **destino** (sucesso) ou, na falha, por exemplo, iniciar uma **função paliativa** ou pôr uma mensagem numa **fila**.
- **Por si só não expõe uma API RESTful**: precisa do **API Gateway** na frente ([[SLS 02 - Custos serverless na AWS]]).

**Custos** ([[SLS 02 - Custos serverless na AWS]])
| Item | Como é cobrado |
|---|---|
| Solicitações | Cada início de execução em resposta a um acionador |
| Duração | Do início ao retorno, arredondada para o 1 ms mais próximo; o preço base sobe com a **memória** |
| Free tier | **1 milhão de solicitações** e **400.000 GB-segundos** por mês |
| Arquitetura | **x86** ou **ARM**, com tabelas diferentes |

- Por isso, Lambdas devem ser **simples e otimizadas**. Na aula 6, "memória e CPUs" são a forma de **precificação**; na aula 2, o custo vem das solicitações e da duração, com preço base pela memória.
- **Criação pelo console**: Container Image · Use a blueprint · Author from scratch (na aula, Node.js 18.x). Para aplicações complexas, o [[AWS SAM]].

Aparece em: [[SLS 01 - Recursos serverless na AWS]], [[SLS 02 - Custos serverless na AWS]], [[SLS 06 - AWS Lambda e AWS SAM]]
