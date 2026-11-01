---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Padrões de projeto, Padrões de design, Design Pattern]
---

# Design Patterns

Soluções **bem estabelecidas e comprovadas** para problemas comuns. Oferecem uma abordagem padronizada, melhoram a reutilização de código e a manutenção, e dão ao time uma **linguagem comum**. Exemplos citados: MVC, Repositório, Factory.

## Padrões de criação
Focam na criação de objetos e instâncias: ocultam a complexidade de criação, garantem que os objetos sejam criados corretamente e centralizam o processo.

| Padrão | Definição |
|---|---|
| **Factory** | Interface para criar objetos numa classe base sem especificar as classes concretas. Permite adicionar classes sem afetar o código existente |
| **Builder** | Separa a construção de um objeto complexo da sua representação: o mesmo processo gera representações diferentes |
| **Singleton** | Garante **uma única instância** da classe, com um ponto de acesso global |
| **Prototype** | Cria novos objetos por **clonagem** de modelos existentes |

## Padrões estruturais
Organizam classes e objetos em estruturas maiores. Simplificam a comunicação entre partes, reduzem a complexidade e aumentam a reutilização. A apostila divide em 3 categorias:

| Categoria | Padrão | Definição |
|---|---|---|
| Adaptação | **Adapter** | Converte a interface de um objeto na interface que o cliente espera, para objetos incompatíveis trabalharem juntos |
| Adaptação | **Bridge** | Separa a abstração da implementação, para que as duas evoluam de forma independente |
| Adaptação | **Proxy** | Objeto representante que controla o acesso a outro objeto |
| Agregação | **Composite** | Compõe objetos em **árvore** para representar hierarquias parte-todo |
| Agregação | **Decorator** | Anexa responsabilidades a um objeto **dinamicamente** |
| Agregação | **Façade** | Interface simplificada para um conjunto de interfaces complexas |
| Composição | **Flyweight** | Minimiza o uso de memória **compartilhando estado** entre objetos idênticos ou semelhantes |
| Composição | **Private Class Data** | Protege a integridade dos dados encapsulando-os numa classe privada |
| Composição | **Bridge** | Mesma definição de antes |

> [!note] Na apostila, o **Bridge** aparece em duas categorias: Adaptação e Composição.

## Padrões de comportamento
Lidam com algoritmos, comunicação e responsabilidades entre objetos, ou seja, como eles interagem. Deixam o software mais flexível e modular.

| Categoria | Padrão | Definição |
|---|---|---|
| Classe | **Template Method** | Esqueleto do algoritmo na superclasse; as subclasses substituem etapas sem mudar a estrutura |
| Classe | **Strategy** | Família de algoritmos encapsulados e **intercambiáveis**; o algoritmo varia independentemente dos clientes |
| Classe | **State** | O objeto muda de comportamento quando o estado interno muda, e parece ter mudado de classe |
| Objeto | **Observer** | Dependência **um-para-muitos**: quando um objeto muda de estado, todos os dependentes são notificados e atualizados |
| Objeto | **Chain of Responsibility** | Vários objetos processam uma solicitação **em cadeia**: cada um processa ou passa adiante |
| Objeto | **Command** | Encapsula a solicitação como objeto: permite parametrizar, enfileirar ou registrar solicitações e suporta **desfazer/refazer** |
| Interação | **Interpreter** | Representação gramatical de um idioma e um interpretador para suas sentenças |
| Interação | **Mediator** | Objeto que encapsula como um conjunto de objetos interage; promove **acoplamento fraco** |
| Interação | **Visitor** | Adiciona novas operações a uma estrutura de objetos **sem modificá-los** |

Aparece em: [[ARQ 01 - Introdução à arquitetura de software]]
