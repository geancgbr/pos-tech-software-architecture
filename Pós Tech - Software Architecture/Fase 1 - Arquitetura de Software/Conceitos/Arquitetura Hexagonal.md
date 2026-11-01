---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Hexagonal Architecture, Arquitetura de Portas e Adaptadores, Ports and Adapters]
---

# Arquitetura Hexagonal

Proposta por **Alistair Cockburn** em meados dos **anos 1990**, num artigo na **WikiWikiWeb**. Aplica a [[Separação de Conceitos (SoC)]] para **diminuir o acoplamento** entre as camadas da aplicação.

## As 3 áreas
| Área | O que tem |
|---|---|
| **Centro do hexágono** (Application) | Modelos, domínio e regras de negócio. Agnóstico a tecnologia, mas pode depender de frameworks gerais (log, IoC). As regras podem ser definidas por **casos de uso** |
| **Lado (superior) esquerdo** | [[Atores Condutores e Conduzidos\|Atores condutores]] e seus adaptadores, que **acionam** o centro |
| **Lado (inferior) direito** | Atores conduzidos e seus adaptadores, **acionados pelo** centro (infraestrutura) |

**Objetivos** (parecidos com os da arquitetura limpa): reusabilidade, alta coesão, baixo acoplamento, independência de tecnologia e facilidade de teste.

**Benefício**: trocar tecnologias (banco, front-end, Web/mobile/API) sem impactar as classes de domínio e os casos de uso.

## O nome
- Não tem relação com o número 6: poderia ser um pentágono ou um heptágono. A ideia é um polígono com vários lados, que são as diferentes implementações e tecnologias.
- Para Cockburn, cada face é um motivo de comunicação com o mundo exterior, por isso hexágonos concêntricos e não círculos.
- Em 2005, ele tentou renomeá-la para **[[Portas e Adaptadores]]**.

## Fluxo e IoC
O fluxo vai do adaptador externo para a porta, a porta executa a lógica de negócio, e a resposta passa por outro adaptador até chegar ao usuário. Com isso, o centro passaria a depender do lado direito. A solução é a [[Inversão de Controle (IoC)]].

> [!warning] "Application" aqui não é a camada de aplicação
> O Application do centro do hexágono é o core, o domínio. Ele **não tem relação** com a camada Application da [[Arquitetura de Camadas]].

## Na disciplina Clean Architecture (Fase 2, aula 2)
- O diagrama hexagonal e o do livro "Arquitetura Limpa" **não são a mesma coisa**, mas compartilham ideias: **Entidades** no centro, **Casos de Uso** com as regras de negócio, e Portas e Adaptadores para o mundo exterior.
- **Input Port**: informa os dados de que o caso de uso precisa. **Output Port**: define como as respostas são entregues. A analogia é uma porta USB.
- **Adapters**: isolam e abstraem um elemento externo (banco, API) e convertem os formatos (ex.: do banco para JSON na Input Port).
- **Diferença**: na Arquitetura Limpa, o que fica fora dos casos de uso se divide em **duas camadas** (interface e adaptadores; e a mais externa). → [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]] · [[Camadas da Arquitetura Limpa]]

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
O serviço **Catálogo de Produtos** é criado sob a **arquitetura hexagonal**, com a classe `CatalogoService`, a lógica em **transaction script** e as **portas e adaptadores de entrada e saída** ([[MS2 01 - Desenhando a lógica de negócios com microsserviços]]).

Na parte 1 da disciplina, a arquitetura hexagonal é citada como estilo aplicado **a um componente** do sistema ([[MS 01 - Estratégias e padrões de microsserviços]]).

## Na disciplina SAGA Pattern (Fase 4)
O projeto de referência usa o estilo **hexagonal** ("não tem relação com as pastas"): **domain** (entidades, exceptions e as **portas** em repository e usecase), **application** (controller REST, DTOs e os **adaptadores de entrada**) e **infra** (os **adaptadores de saída**) ([[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]).

Aparece em: [[ARQ 05 - Arquitetura Hexagonal]], [[MS2 01 - Desenhando a lógica de negócios com microsserviços]], [[MS 01 - Estratégias e padrões de microsserviços]], [[SAGA 04 - Aplicando o padrão SAGA na prática, parte 1]]
