---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 1
fonte: "Aula 1.pdf (Erick Muller)"
---

# CA 01 - Introdução e SOLID

[[Clean Architecture]] · Próxima → [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]]

> [!summary] Em uma frase
> A **Arquitetura Limpa** (Robert C. Martin) não é métrica, certificação nem padrão de projeto. É um conjunto de ideias para um código **fácil de entender, manter e alterar**, organizado em componentes e **camadas como as de uma cebola**. O **[[SOLID]]** guia como cada unidade de código deve ser construída.

## Hands On
Uma discussão mais prática, com comparações do dia a dia, sobre formas de implementar o SOLID e sobre por que o código limpo é importante num projeto de longo prazo.

## Arquitetura de software e Arquitetura Limpa
- Arquitetura de software é um campo amplo, baseado **parte em estudo e parte em análise de casos**. Como criar software é uma disciplina nova, as práticas ainda não estão solidificadas, e isso é uma oportunidade de aprender formas diferentes de resolver o mesmo problema.
- Quanto **maior a base de código**, melhor deve ser a estrutura, os testes, as definições das regras de negócio e os processos.
- A Arquitetura Limpa é **difícil de definir**, porque não está ligada a uma métrica nem a um "atestado de qualidade". Mas é **fácil identificar** um código com ou sem ela, e isso fica mais fácil com a experiência.
- Robert Martin, desde **"Clean Code"** e **"Clean Coder"**, define boas práticas para um software fácil de manter e de entender, com **limites bem definidos entre as camadas**, usando recursos da linguagem (por exemplo, **interfaces e herança**, da orientação a objetos) para ter **pouco acoplamento**.
- **Sem essa organização, metodologias ágeis ficam complicadas**, porque não dá para aplicar agilidade num código difícil de manter.

## Mitos e verdades
| A Arquitetura Limpa... | Segundo a apostila |
|---|---|
| gera código mais conciso, com menos classes? | **Não.** Gera **mais** código, porque é preciso criar unidades que isolem responsabilidades |
| usa técnicas de programação complicadas? | **Não.** Baseia-se em regras de codificação e de arquitetura |
| deixa tudo explícito? | **Sim.** Um princípio da boa arquitetura é que nada cause dúvida na implementação ou na manutenção |

- **Legibilidade**: lemos muito mais código do que escrevemos. Um bloco único é mais difícil de entender do que componentes distribuídos, **mas componentes mal estruturados podem ser ainda piores**, com erros espalhados por vários pedaços.
- **Componentes especializados**, com responsabilidades únicas e bem definidas. Nada de classes generalistas.
- **Camadas** são grupos de componentes com responsabilidades semelhantes. Exemplo: na camada de **Casos de Uso** não pode haver código de conexão com banco de dados. Por isso o projeto é visto como **camadas de uma cebola**, e não de um bolo. Detalhes em [[Camadas da Arquitetura Limpa]].

## SOLID
| Letra | Princípio | O que define | Exemplo ou analogia da aula |
|---|---|---|---|
| **S** | Responsabilidade Única (*Single Responsibility*) | Uma unidade tem **uma responsabilidade** e **um único motivo para mudar**. Não pode, por exemplo, alterar a resposta conforme o tipo de chamada | O **atendente de lanchonete**: anota o pedido, passa para a cozinha, registra o pagamento e entrega. É a interface entre cliente e cozinha, do mesmo jeito para todos |
| **O** | Aberto-Fechado (*Open-closed*) | Aberto para **extensão**, fechado para **alteração**: uma nova funcionalidade estende o que existe, sem mexer nele | Novo formato de **relatório**: separar o código que gera os dados dos tipos de relatório, em vez de colocar mais uma condição na função existente |
| **L** | Substituição de Liskov (*Liskov Substitution*) | Uma classe pode ser substituída por outra do tipo base sem problemas para o software. A melhor forma de implementar é com **interfaces** | O código que usa a classe não deve depender de métodos que só existem numa das classes filhas |
| **I** | Segregação de Interface (*Interface Segregation*) | Uma classe não deve implementar interfaces e métodos que não implementará. Interfaces mais **enxutas e focadas**; pensar nos componentes pelo **comportamento**, não pela implementação | A **tomada**: o dispositivo não se importa com a instalação elétrica, só com a tensão certa chegando pela mesma interface |
| **D** | Inversão de Dependência (*Dependency Inversion*) | Um módulo de **alto nível não depende de um de baixo nível** (segundo a aula, os níveis se referem sempre aos módulos mais perto da infraestrutura). Uma abstração não depende de detalhes de implementação; depende-se de **abstrações (interfaces)** | Um cálculo que precisa de uma origem de dados não deve depender de uma implementação única dessa origem |

> [!warning] Inversão de dependência ≠ injeção de dependência
> **Inversão** é entregar ao usuário o que ele vai usar sem que ele se importe com como foi criado. **Injeção** é **um dos métodos** usados para isso: injetar o componente para o código usar.

## Resumo da própria apostila
- A arquitetura ("simples", como está escrito no resumo do PDF) não é certificação nem padrão de projeto: é um conjunto de ideias e recomendações. Gera mais código, porque isola responsabilidades.
- **O SOLID diz como cada unidade deve ser construída; a Arquitetura Limpa diz como organizar e pensar a responsabilidade e a interação entre essas unidades.**

## Referências
*Clean Code e Solid* (YouTube, 2021) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008) · Martin, *The Clean Coder* (2011)
