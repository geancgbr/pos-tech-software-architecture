---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Caso de Uso, Use Case, Use Cases]
---

# Casos de Uso

**Como ferramenta**: a documentação de um processo de negócio, com os dados necessários, os passos, as **exceções** e como tratá-las, e o **resultado**. Nas metodologias ágeis, faz implementar **só o necessário, não o desejado**, e por isso os cards costumam se basear em casos de uso.

**Como camada da Arquitetura Limpa**: fica entre Entidades e Controllers. É o **"cérebro"**, que centraliza as regras de negócio.

**Regras**
- **Um caso de uso por implementação**; casos complexos se dividem em menores, com chamadas **explícitas** entre eles.
- Só usa **outros casos de uso e entidades**.
- Agrupamento coerente em pacotes ou classes (com **métodos estáticos**, **sem dividir estado**).
- Usa **entidades** como abstração dos atores, nunca os dados crus.
- Recebe as dependências (repositórios, Gateways) por **injeção de dependência e interfaces**.

**As três partes**: dados recebidos · algoritmo interno · retorno (uma entidade ou um objeto de dados, DAO).

**Teste**: com um **[[Mock|mock]]** do repositório, as regras são testadas antes de conectar às interfaces de comunicação externa.

> [!warning] "O que" × "como"
> A aula 4 diz em um trecho que os casos de uso definem o "como". O resumo da mesma aula isola "o que" o software faz com os casos de uso e as entidades. A aula 3 trata as camadas internas como o "o que", e a aula 7 chama de "quê" os componentes das regras de negócio.

Aparece em: [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]], [[CA 03 - Camada de entidades]], [[CA 04 - Camada de casos de uso]], [[CA 08 - Revisão da disciplina]]
