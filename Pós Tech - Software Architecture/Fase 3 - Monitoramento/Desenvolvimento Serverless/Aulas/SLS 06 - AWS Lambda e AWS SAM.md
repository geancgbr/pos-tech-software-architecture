---
tags: [pos-tech/fase-3, serverless, aws, aula]
disciplina: Desenvolvimento Serverless
aula: 6
fonte: "Desenvolvimento Serverless/Desenvolvimento Serverless - Aula 6.pdf (Luiz Zenha)"
---

# SLS 06 - AWS Lambda e AWS SAM

← [[SLS 05 - Amazon Cognito e OAuth 2.0]] · [[Desenvolvimento Serverless]]

> [!summary] Em uma frase
> O **[[AWS Lambda]]** executa código **em resposta a eventos** (triggers como API Gateway, IoT, S3, SNS e SQS), com funções pequenas e de **responsabilidade única**, e pode ter um **destino** em caso de sucesso ou falha. Para aplicações mais complexas, o **[[AWS SAM]]** (Serverless Application Model) ajuda a **criar, testar localmente e implantar**, ao custo de **acoplamento com a AWS**.

## Hands On
A teoria do Lambda (funcionamento por **triggers**) e do **SAM CLI**, que ajuda na **padronização** dos projetos Lambda e no **teste local**. Na prática:
1. Revisar a instalação do **SAM**.
2. Criar um projeto Lambda em **Java**.
3. Rodar **localmente** (a vantagem do SAM para depurar).
4. **Deploy** com o SAM.
5. Testar integrado ao **API Gateway**.

Segundo o "O que vem por aí", também se cria um Lambda simples com **NodeJS**. A vantagem de custo do Lambda está em **APIs com picos de uso** ou **tarefas em alguns horários**.

## AWS Lambda
- Serviço de **computação serverless** da AWS: executar código **sem provisionar ou gerenciar servidores**, em resposta a **eventos** (alterações em bancos, uploads, chamadas de API e outros).
- Baseado em **funções**: códigos pequenos, que normalmente têm **uma única responsabilidade**, **independentes**, em **Node.js, Python, Java, C#** e outras linguagens.
- "Geralmente, quando pensamos em serverless, o AWS Lambda é a primeira resposta!" O serviço gerencia o **provisionamento e a escalabilidade** conforme a demanda; resta definir **memória e CPUs**, que são a forma de **precificação**.
- **Funcionamento**: sempre há um **trigger** que invoca a função. Ao terminar, ela **pode ou não ter um destino**, chamado no **sucesso**; na **falha**, pode, por exemplo, iniciar uma **função paliativa** ou pôr uma mensagem numa **fila**.

| Trigger | O que dispara |
|---|---|
| **API Gateway** | Invocação por API |
| **AWS IoT** | Dispositivos IoT |
| **S3** | Chegada de um arquivo |
| **SNS e SQS** | Nova mensagem numa fila ou tópico |

**Cenários (com a empresa de eventos)**
| Cenário | Exemplo do PDF |
|---|---|
| **Processamento de arquivos** | Upload de imagens num bucket **S3** dispara um Lambda que adiciona **marca d'água**, gera os tamanhos e salva em outro bucket usado pelo site (Figura 1) |
| **Dados e análise** | Gravações, atualizações e exclusões numa tabela **DynamoDB** **poderão** publicar eventos pelos **DynamoDB Streams** (chave do item, nome do evento e detalhes); pode-se escrever um Lambda que gere **métricas personalizadas**, cruzando, por exemplo, com um **CRM** |
| **Sites** | O cenário da aula: uma API com Lambda que expõe os eventos para o calendário do front-end, invocada por HTTP via **API Gateway** (Figura 2) |
| **Aplicações móveis** | É possível configurar um Lambda para processar eventos publicados pela aplicação, como os **cliques** |

**Criando pelo console**: buscar "Lambda" → **Functions** → **Create function**, com três opções: **"Container Image"** (a partir de uma imagem), **"Use a blueprint"** (modelos prontos com integrações como S3, Cognito, API Gateway) e **"Author from scratch"** (nome e linguagem; na aula, **Node.js 18.x**). Dá para ajustar **permissões** para triggers e destinations. Depois, aba **"Test"** com um evento de teste (Figuras 3 a 5).

> [!note] O texto chama de "nosso primeiro Lambda" o criado pelo console (Node.js); o resumo diz que a primeira função Lambda foi criada "com o AWS SAM CLI".

## AWS SAM
- **Framework open source** e amplamente usado para **desenvolver, testar e implantar** aplicativos serverless na AWS, com uma estrutura para **descrever e organizar** recursos e funções.
- **Vantagens**: **simplicidade**; usa a sintaxe **YAML do CloudFormation**; traz **exemplos de projetos** (bom para quem está começando). O **SAM CLI** cria, testa e implanta pela linha de comando, e o SAM é **integrado ao AWS CodePipeline**, para **implantação contínua**.
- **Pré-requisitos**: **AWS CLI** instalado e configurado (credenciais no **AWS IAM Identity Center**) e **Docker** (para executar e testar localmente).
- **Validar a instalação**: `sam`. Depois, criar um projeto com um **modelo pré-definido** ou próprio; o modelo traz as instruções de **CloudFormation** (funções Lambda, APIs, tabelas DynamoDB e outros).
- **Teste local**: o SAM CLI **emula o ambiente da AWS** na máquina, útil para depurar antes da implantação.
- **Desvantagem**: por ser **específico da AWS**, pode restringir a **portabilidade**; cria um **grande acoplamento** com a AWS, e migrar de provedor exige **reconstruções**.

## Referências
AWS: AWS Serverless Application Model · Tipos de aplicações e casos de uso comuns do Lambda · What is AWS Lambda?
