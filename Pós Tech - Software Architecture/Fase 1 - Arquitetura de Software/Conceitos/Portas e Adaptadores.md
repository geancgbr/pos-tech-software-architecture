---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Porta, Portas, Adaptador, Adaptadores, Ports, Adapters, Porta de entrada, Porta de saída]
---

# Portas e Adaptadores

## Porta
- **Conceito lógico** que define um **ponto de entrada e saída** da aplicação.
- São as **interfaces de programação** usadas para falar com os casos de uso (interface no sentido de programação, como em C#: `public interface ICadastroPessoa{}`).
- São **independentes de tecnologia**, por isso ficam **no centro do hexágono**.

Os dois tipos, segundo Marco Tulio Valente (*Engenharia de Software Moderna*):

| Tipo | Direção | Declara | Exemplo |
|---|---|---|---|
| **Porta de entrada** | De fora para dentro: uma classe externa chama um caso de uso | Serviços **providos** pelo sistema ao mundo exterior | Não se aplica |
| **Porta de saída** | De dentro para fora: uma classe de domínio chama uma classe externa | Serviços **requeridos** do mundo exterior | Interação com banco de dados |

## Adaptador
- São as **tecnologias do lado de fora** do hexágono: HTTP/REST, gRPC, GraphQL, SQL, NoSQL, aplicativo web ou mobile.
- **Função**: implementar a conexão entre uma porta e os serviços externos.
- Funcionam como "plugues", como um adaptador de tomada ("Benjamin" ou "T").
- **Regra**: **pelo menos dois adaptadores por porta**, um para **teste** e um para a **implementação real**.
- **Exemplo**: uma porta de cache com um adaptador **Redis** e outro de **cache em memória** (para testes unitários).

Os atores condutores encaminham as chamadas para as portas de entrada. Os atores conduzidos são acionados pelo centro do hexágono por meio das portas secundárias. → [[Atores Condutores e Conduzidos]] Visão geral em [[Arquitetura Hexagonal]].

Aparece em: [[ARQ 05 - Arquitetura Hexagonal]]
