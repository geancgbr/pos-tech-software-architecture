---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 8
fonte: "Aula 8.pdf (Erick Muller)"
---

# CA 08 - Revisão da disciplina

← [[CA 07 - Detalhes - dados, acesso e frameworks]] · [[Clean Architecture]]

> [!summary] Em uma frase
> Recapitulação: o **[[SOLID]]** é a base, e as **4 camadas** (Entidades, Casos de Uso, Adaptadores de Interface, Frameworks e Drivers) seguem duas regras de interação. Os recursos externos são **serviços**, não dependências: são **detalhes**.

## Hands On
Uma implementação de código mostrando como as regras da Arquitetura Limpa aparecem na codificação. O PDF traz um link para uma base de dados da aula.

## Por que uma boa arquitetura
Construir software é difícil. Com qualidade, mais difícil ainda. Com qualidade e fácil de alterar e entender, tende a ser uma tarefa exaustiva e muitas vezes demorada. Parte do profissionalismo é produzir código, e a outra parte é a **perícia em criar código de alta qualidade no tempo adequado**. A Arquitetura Limpa oferece **ideias que funcionam como heurística** para as decisões, mais do que dizer onde vai cada componente.

## SOLID, na versão da revisão
| Letra | Como a aula 8 resume |
|---|---|
| **S** | Nenhum componente faz mais de uma coisa: **uma responsabilidade** e **um tipo de requisição** |
| **O** | Fechado para alteração, aberto para extensão. Nova funcionalidade num **novo componente**. O original deve permitir uso por **herança ou composição** |
| **L** | Uma classe derivada pode ser substituída pela classe base sem o software parar. Assim, uma classe não depende indiretamente de um comportamento da derivada, o que dá mais segurança para injetar dependências |
| **I** | Uma classe não depende de comportamento que não usa. As dependências seguem a **interface**, não um objeto específico. É útil na injeção de dependências e na comunicação por protocolos |
| **D** | Um objeto de mais alto nível não depende diretamente de um de mais baixo nível. Quem implementa detalhes depende só de **abstrações**. O componente x depende só da interface do y e o **recebe como dependência** no momento do uso |

## As 4 camadas (Figura 1: diagrama de referência, Martin 2019)
| Camada (de dentro para fora) | Responsabilidade | Exemplos (escola) |
|---|---|---|
| **Entidades** | Elementos únicos da regra de negócio: encapsulam os dados, garantem o **estado interno consistente** (validação em todo o ciclo de vida) e validam a colaboração com outras entidades | Estudante, Disciplina, Docente, Avaliação |
| **Casos de Uso** | Um componente por caso de uso. Usa os dados das camadas externas, **instancia as entidades**, executa e responde a quem pediu | Aplicar Avaliação, Matricular Estudante em Disciplina |
| **Adaptadores de Interface** | Dão às camadas externas o acesso aos casos de uso: **Controllers** (recebem, preparam e executam), **Gateways** (abstraem o acesso a dados) e **Adapters** (usados pelos Controllers para formatar o retorno) | Não há na apostila |
| **Frameworks e Drivers** | Acesso aos recursos externos: APIs abertas a usuários, repositórios de dados, serviços externos | Não há na apostila |

> [!warning] Presenters (aula 5) × Adapters (aula 8)
> Na aula 5, os três componentes dos Adaptadores de Interface são **Controllers, Presenters e Gateways**. Na aula 8, são **Controllers, Gateways e Adapters**, e o papel descrito para o "Adapter" (formatar o retorno do Controller) é o mesmo que a aula 5 dá ao **Presenter**.

## As duas regras de interação
1. **Componentes internos não dependem diretamente nem acessam componentes externos.** Se precisarem, recebem o componente por **injeção de dependência**, e o componente interno define uma **interface** para "receber" o externo.
2. **Componentes da mesma camada podem interagir e depender entre si.** Um caso de uso pode chamar outro, e um Controller usa um Adapter para preparar a resposta.

Os recursos externos são **serviços externos, não dependências**: são vistos como **detalhes**. Assim a Arquitetura Limpa entrega um software **escalável**, de alta qualidade de funcionamento e manutenção.

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008)
