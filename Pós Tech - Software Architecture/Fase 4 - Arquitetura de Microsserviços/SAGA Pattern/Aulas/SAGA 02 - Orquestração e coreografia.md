---
tags: [pos-tech/fase-4, microsservicos, saga, aula]
disciplina: SAGA Pattern
aula: 2
fonte: "SAGA Pattern/Aula 2 - Padrão SAGA - Orquestração e coreografia.pdf"
---

# SAGA 02 - Orquestração e coreografia

← [[SAGA 01 - Introdução ao padrão SAGA]] · [[SAGA Pattern]] · Próxima → [[SAGA 03 - Lidando com a falta do I do ACID]]

> [!summary] Em uma frase
> Quem coordena a ordem dos serviços e as compensações numa SAGA? Na **coreografia**, a decisão é **distribuída** entre os participantes, que trocam **eventos** (como uma dança); na **orquestração**, um **orquestrador** envia **comandos** (como um maestro). Segundo **Chris Richardson**, a coreografia é mais recomendada para **SAGAs simples**; nos demais cenários, a orquestração **tende** a ser mais benéfica. A aula cita **Google Cloud Workflows** e **AWS Step Functions**. Ver [[Saga]].

## Hands On (vídeos)
Nas videoaulas: as formas de implementação do padrão SAGA, **orquestrada** e **coreografada**.

## A SAGA como composição de membros
- Uma SAGA é a composição de vários serviços que atuam como **membros** (Figura 1, trecho com uma **ação compensatória**).
- É definida uma **sequência lógica** tanto para o **caminho feliz** (todas as operações com sucesso) quanto para quando um membro não se comporta como esperado.

## Coreografia × orquestração
| | **Coreografia** | **Orquestração** |
|---|---|---|
| Analogia | Uma **dança**: cada participante conhece seus passos e se comunica por **mensagens** (Figura 2) | Um **maestro** conduzindo a orquestra (Figura 4) |
| Quem decide | Responsabilidade **distribuída** entre os participantes | Um **componente de orquestração** envia **comandos** dizendo o que executar |
| Diagrama | Figura 3: criação de pedido com **mensageria** | Figura 4 (segunda): criação de pedido orquestrada |
| **Prós** | **Simplicidade**: os serviços publicam **eventos** quando seu estado muda e os outros reagem, sem saber como são implementados · **Acoplamento fraco**: publicam e consomem por um **intermediário** (ex.: barramento de mensagens); cada serviço **pode** ser desenvolvido e implantado de forma **independente** | **Simplificação das dependências**: requisições em **mão única**, sem os **riscos** de dependências cíclicas · **Acoplamento fraco**: cada serviço expõe uma **API** consumida pelo orquestrador · **Menos complexidade na lógica de negócio**: orquestração **centralizada**; os serviços **desconhecem** as Sagas de que fazem parte |
| **Contras** | **Mais difícil de entender**: não há um único lugar no código que define a Saga · **Dependências cíclicas**: os participantes assinam os eventos uns dos outros, o que **geralmente** cria ciclos e **pode** causar **recursão infinita** · **Risco de forte acoplamento**: cada participante assina **todos os eventos que o afetam** | **Orquestrador complexo**: com muitas regras de negócio, **pode** ficar difícil de manter · **Ponto único de falha**: a falha do orquestrador afeta toda a SAGA |

> [!warning] Inconsistências do PDF
> - Há **duas Figuras 4**: o maestro e a SAGA orquestrada.
> - Na coreografia, "acoplamento fraco" aparece nos prós e "risco de forte acoplamento" nos contras.
> - O texto diz que a falha do orquestrador "vai **disponibilizar** toda a SAGA"; pelo contexto (ponto único de falha), o sentido é **indisponibilizar**.

## Implementações em nuvem
- **Google Cloud Workflows**: aplicar o padrão Saga no contexto de Workflows; o conteúdo está **só na Figura 5** e no site do Google Cloud.
- **AWS Step Functions** (Figura 6): processamento de pedidos em que cada etapa (ex.: **"ProcessPayment"**) tem etapas separadas para o **sucesso** (ex.: **"UpdateCustomerAccount"**) ou a **falha** (ex.: **"SetOrderFailure"**).

## O que você viu
- As duas estratégias oferecem benefícios para transações distribuídas numa malha de serviços, e ambas têm **contras** cujo risco deve ser considerado na decisão.
- Segundo **Chris Richardson** (*Microservices Patterns*), a **coreografia** é mais recomendada para **SAGAs simples**; nos outros cenários, a **orquestração tende** a ser mais benéfica.

## Referências
AWS: Saga Pattern (Prescriptive Guidance) · Richardson, *Microservices Patterns* · Universidade Cornell: Sagas (2002)
