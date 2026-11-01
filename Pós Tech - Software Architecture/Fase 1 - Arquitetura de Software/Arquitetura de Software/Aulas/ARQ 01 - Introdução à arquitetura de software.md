---
tags: [pos-tech/fase-1, arquitetura, aula]
disciplina: Arquitetura de Software
aula: 1
fonte: "Aula 1 - Arquitetura de Software_revFinal.pdf"
---

# ARQ 01 - Introdução à arquitetura de software

[[Arquitetura de Software]] · Próxima → [[ARQ 02 - Processo e modularização]]

> [!summary] Em uma frase
> A [[O que é Arquitetura de Software|arquitetura de software]] é a estrutura lógica e física de um sistema (componentes, interações e restrições de design). A aula apresenta o livro [[Clean Architecture (livro)|Clean Architecture]], os [[Design Patterns]] e a [[Arquitetura de Camadas]].

## Hands On (vídeos)
- A importância do papel do(a) arquiteto(a) para planejar um projeto estruturado, manutenível e, principalmente, escalável.
- Analogia do pedreiro com a pessoa desenvolvedora: organizar-se sempre com uma **documentação mínima** e uma **estratégia** antes de construir.
- Exemplo real: um projeto desenvolvido para a TV Bandeirantes.

## Arquitetura de software
- **Definição**: estrutura lógica e física de um sistema, incluindo **componentes**, **interações** e **restrições de design**. Determina como o sistema deve ser construído e como os componentes se integram.
- **Por que estudar**: afeta como o sistema é criado, desenvolvido, mantido e evoluído, e afeta a qualidade em **flexibilidade, escalabilidade, desempenho e segurança**.
- **Fatores a considerar**: requisitos de negócio, restrições de tempo e orçamento, padrões de design e tecnologias.
- **Principais considerações**: separação de preocupações, modulação, reutilização de componentes e escolha de padrões de design apropriados.
- **Abordagens**: baseada em **camadas**, em **componentes** e em **serviços**. Cada uma tem vantagens e desvantagens, e a escolha depende das necessidades do projeto e do contexto.
- **Outros tópicos comuns**: escolha de tecnologias, criação de modelos de arquitetura, avaliação e seleção de arquiteturas, documentação de arquiteturas e gerenciamento de mudanças ao longo do tempo. Esses pontos garantem que o projeto tenha estrutura **desde o dia 0** e seja escalável e manutenível.

Detalhes em [[O que é Arquitetura de Software]].

## Livro recomendado: Clean Architecture (Robert C. Martin, "Uncle Bob")
Guia para criar sistemas de alta qualidade, de forma mais eficiente e sustentável. Os principais pontos: separação de preocupações, responsabilidade única, abstração, depuração fácil e simplicidade. Veja [[Clean Architecture (livro)]].

## Tópicos comuns de arquitetura
- **[[Design Patterns]]**: soluções geralmente aceitas para problemas comuns (por exemplo, MVC, Repositório, Factory).
- **Microservices**: divide a aplicação em pequenos serviços independentes que trabalham juntos para fornecer uma solução completa.
- **[[Arquitetura de Camadas]]**: estrutura o software em camadas lógicas, cada uma responsável por uma funcionalidade.

## Design patterns: 3 categorias
| Categoria | Foco | Padrões citados |
|---|---|---|
| **Criação** | Criação de objetos e instâncias | Factory, Builder, Singleton, Prototype |
| **Estruturais** | Organizar classes e objetos em estruturas maiores | Adaptação, agregação e composição |
| **Comportamento** | Algoritmos, comunicação e responsabilidades entre objetos | Classe, objeto e interação |

A lista completa, com a definição de cada padrão, está em [[Design Patterns]].

## Arquitetura de camadas
- O sistema é dividido em camadas (níveis lógicos), organizadas numa **pilha**: as **mais baixas fornecem serviços** para as **mais altas**.
- As camadas mais comuns são **apresentação/interface do usuário**, **aplicação** (lógica de negócios) e **persistência de dados**. Algumas implementações acrescentam camada de serviços ou de infraestrutura.
- **Objetivo**: separar as preocupações em níveis de abstração, para que cada camada seja implementada, testada e mantida de forma independente.

Detalhes em [[Arquitetura de Camadas]].

## Referência
Bass, Clements e Kazman. *Software Architecture in Practice*, 3ª ed., 2012.
