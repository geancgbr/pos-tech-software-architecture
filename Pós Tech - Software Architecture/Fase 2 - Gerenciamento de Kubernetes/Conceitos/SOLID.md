---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Princípios SOLID, SRP, OCP, LSP, ISP, DIP, Responsabilidade Única, Aberto-Fechado, Substituição de Liskov, Segregação de Interface, Inversão de Dependência]
---

# SOLID

Acrônimo, em inglês, de **cinco princípios** definidos nos livros *Clean Code* e *Clean Architecture*, de Robert C. Martin. É um guia de código de qualidade e a **base de toda a Arquitetura Limpa**: o SOLID diz como cada unidade deve ser construída, e a Arquitetura Limpa diz como organizar as unidades e a interação entre elas.

| | Princípio | Aula 1 | Aula 8 |
|---|---|---|---|
| **S** | **Responsabilidade Única** | Uma responsabilidade e **um único motivo para mudar** (ex.: atendente de lanchonete) | Nenhum componente faz mais de uma coisa; atende **um tipo de requisição** |
| **O** | **Aberto-Fechado** | Permite **extensão**, não **alteração** (ex.: novo formato de relatório sem mais um `if`) | Nova funcionalidade num **novo componente**; o original permite uso por **herança ou composição** |
| **L** | **Substituição de Liskov** | Uma classe pode ser substituída por outra do tipo base sem problemas; implemente com **interfaces** | A classe derivada pode ser substituída pela base sem o software parar; mais segurança para injetar dependências |
| **I** | **Segregação de Interface** | Não implementar interfaces e métodos que não implementará; interfaces **enxutas**; pensar no **comportamento** (ex.: tomada) | Não depender de comportamento que não usa; depender da **interface**, não do objeto |
| **D** | **Inversão de Dependência** | Alto nível não depende de baixo nível (os níveis se referem aos módulos mais perto da infraestrutura); dependa de **abstrações** | O componente x depende só da interface do y e o **recebe como dependência** no uso |

> [!warning] Inversão ≠ injeção de dependência (aula 1)
> **Inversão de dependência**: passar ao usuário o que ele vai usar sem que ele se importe com como foi criado. **Injeção de dependência**: um dos métodos usados para isso.

Na prática da Arquitetura Limpa, a inversão de dependência permite passar a um caso de uso um **repositório "falso"** para teste ([[Casos de Uso]], [[Mock]]).

Aparece em: [[CA 01 - Introdução e SOLID]], [[CA 04 - Camada de casos de uso]], [[CA 08 - Revisão da disciplina]]
