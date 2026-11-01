---
tags: [pos-tech/fase-1, ddd, conceito, design-tatico]
aliases: [Value Object, Objetos de Valor, VO]
---

# Objeto de Valor

Objeto **sem identificador**, distinguido pelos seus **valores**. É **imutável**.

Características (Vernon):
1. mede, quantifica ou descreve algo do domínio;
2. pode ser mantido imutável;
3. é um **todo conceitual**: os atributos formam uma unidade;
4. é **substituído por inteiro** quando a medida ou descrição muda;
5. é comparado por **igualdade de valores**.

Analogia da aula: se `x = 3` vira `4`, você não altera o 3, cria outro valor. Numa lista de objetos de valor, inserir um item com valores repetidos não cria nada novo, porque ele já existe.

Contraste: [[Entidade]] tem ID e é mutável.

Aparece em: [[DDD 05 - Implementando arquitetura e lógica]]
