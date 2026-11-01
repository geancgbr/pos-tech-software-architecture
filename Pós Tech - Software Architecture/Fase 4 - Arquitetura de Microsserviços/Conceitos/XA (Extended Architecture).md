---
tags: [pos-tech/fase-4, microsservicos, saga, conceito]
aliases: [XA, Extended Architecture, Transaction Manager]
---

# XA (Extended Architecture)

Especificação publicada pela **X/Open** nos **anos 90** para transações distribuídas, delegando a gestão a um **Transaction Manager**. Vários SGBDs (**mas não todos**) a adotaram, como **Oracle** e **MySQL** ([[SAGA 01 - Introdução ao padrão SAGA]]).

- Problemas: **locks distribuídos** entre as bases; com o Transaction Manager **indisponível**, os locks ficavam mantidos até sua recuperação; em casos críticos, **intervenções manuais**.
- Antes disso, nos anos 80, a tática comum era o **lock de objetos no banco**, que garantia consistência mas prejudicava a velocidade; daí a proposta da [[Saga]] em 1987.

Aparece em: [[SAGA 01 - Introdução ao padrão SAGA]]
