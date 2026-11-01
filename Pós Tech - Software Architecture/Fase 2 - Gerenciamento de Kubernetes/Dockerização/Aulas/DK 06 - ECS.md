---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 6
fonte: "Aula 06- ECS.pdf"
---

# DK 06 - ECS

← [[DK 05 - Segurança de contêineres]] · [[Dockerização]]

> [!summary] Em uma frase
> O [[ECS (Elastic Container Service)|ECS (Elastic Container Service)]] é o serviço da **AWS** para **executar, escalar e gerenciar contêineres Docker** num cluster de servidores. Os conceitos centrais são **cluster, tarefa (com definição de tarefa) e serviço**, rodando em **EC2 ou Fargate** e integrados a IAM, CloudWatch e ELB.

## Hands On
O professor demonstra o ECS num exemplo prático e próximo do dia a dia, com casos e configurações passo a passo.

## Conceitos fundamentais
| Conceito | O que é |
|---|---|
| **Contêineres e imagens** | Contêineres são **unidades leves e portáteis** que executam a aplicação de forma consistente em qualquer ambiente. Imagens Docker são **"instantâneos"** da aplicação, com código, runtime, bibliotecas e configurações |
| **Cluster** | **Conjunto lógico de instâncias EC2 ou de tarefas Fargate**. Pode ter várias tarefas e serviços: é o ambiente onde os contêineres rodam |
| **Tarefa** | A **menor unidade de execução** do ECS. É definida por uma **definição de tarefa**, que especifica imagem Docker, CPU, memória, portas de rede e variáveis de ambiente |
| **Serviço** | Mantém uma **quantidade específica de tarefas** rodando ao mesmo tempo, **reinicia** as que falham e pode **balancear a carga** entre as instâncias |

## Benefícios com outros serviços AWS
1. **Integração com a AWS**: **IAM** (controle de acesso), **CloudWatch** (monitoramento) e **ELB** (balanceamento de carga).
2. **Escalabilidade**: **auto-scaling** das tarefas por métricas de **CPU e memória**.
3. **Flexibilidade de execução**:
   - **EC2**: mais **controle** sobre as instâncias;
   - **Fargate**: **serverless**, sem precisar gerenciar servidores.
4. **Segurança**: políticas de **IAM** e **VPCs** para isolar e proteger os recursos.

## Fluxo de credenciais no ECS (Figura 1, fonte AWS)
1. **Buscar as credenciais da instância**: a instância do cluster obtém suas credenciais no **serviço de metadados do EC2**.
2. **Buscar as credenciais de função**: o **agente do ECS** usa as credenciais da instância para buscar as credenciais de função.
3. **Iniciar o contêiner e definir o segredo do contêiner**: o agente inicia uma tarefa e define o segredo, fornecendo as credenciais necessárias.
4. **Buscar as credenciais da tarefa com o segredo do contêiner**: a tarefa usa o segredo para buscar suas próprias credenciais.

## Casos de uso
| Caso | Por que o ECS ajuda |
|---|---|
| **Desenvolvimento e teste** | Ambientes consistentes, criados e destruídos rapidamente |
| **Microsserviços** | Gerencia e orquestra vários contêineres, cada um com um serviço, o que melhora a escalabilidade e a manutenção |
| **Aplicações de alto desempenho** | Aplicações que exigem alta disponibilidade e desempenho aproveitam a escalabilidade automática e o balanceamento de carga, com uma experiência de usuário contínua e eficiente |
| **Big Data e processamento em lote** | Tarefas em lote e pipelines de dados, escaláveis e econômicos |

## Referências
Alura, *Diferença entre o EC2 e o ECS* (2023) · AWS, *Alocação de CPU no Amazon ECS* (2020) · Ilegra, *Desmistificando a orquestração de containers com o ECS* (2023)
