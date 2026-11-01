---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Modularização de sistemas, Módulos]
---

# Modularização

Técnica de design em que o sistema é dividido em **módulos independentes**, cada um com uma função específica, que podem ser **desenvolvidos, testados e mantidos separadamente**.

**Vantagens**
- Mais fácil de entender: cada módulo tem uma função.
- Mais fácil de modificar e atualizar sem afetar o resto.
- Mais flexível: novos módulos entram sem afetar o restante.
- Melhor qualidade: erros são detectados e corrigidos módulo a módulo.
- Desenvolvimento mais eficiente: equipes trabalham em módulos diferentes ao mesmo tempo.

**Cuidados**
- Interfaces entre os módulos **claras e bem definidas**.
- Organização **lógica e coerente** dos módulos, com planejamento cuidadoso.

**Exemplos da aula**
- E-commerce: módulos de pedidos, pagamentos e estoque. O de pagamentos consulta o de pedidos antes de marcar um pedido como "processado".
- REC (Hands On): módulos de Usuários, Canais e Redes sociais.

Aplica-se a e-commerce, gestão de estoque, sistemas bancários e outros.

Aparece em: [[ARQ 02 - Processo e modularização]]
