---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [IoC, Inversion of Control, Inversão de Controle]
---

# Inversão de Controle (IoC)

Princípio de design em que a **sequência (o controle) das chamadas de métodos é invertida** em relação à programação tradicional: ela **não é determinada diretamente pelo programador**.

- O controle é **delegado a uma infraestrutura de software**, muitas vezes chamada de **contêiner**, ou a outro componente que assume a execução. É comum em frameworks.
- É um padrão utilizado em projetos **orientados a objetos**, que utilizam conceitos como **interface, herança e polimorfismo**.

**Na [[Arquitetura Hexagonal]]**: no fluxo de execução, o centro do hexágono passaria a depender do lado direito (dos atores conduzidos). Cockburn aplicou a IoC para resolver esse problema.

O centro do hexágono pode depender de frameworks de serviços gerais, como IoC e log.

Aparece em: [[ARQ 05 - Arquitetura Hexagonal]]
