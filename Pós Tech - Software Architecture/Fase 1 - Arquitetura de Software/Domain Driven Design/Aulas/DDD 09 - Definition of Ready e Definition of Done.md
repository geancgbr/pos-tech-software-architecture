---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 9
fonte: "Aula 09- Definition of Ready e Definition of Done.pdf"
---

# DDD 09 - Definition of Ready e Definition of Done

← [[DDD 08 - Refinamento técnico]] · [[Domain Driven Design]]

> [!summary] Em uma frase
> A [[Definition of Ready e Definition of Done|DoR]] é o portão de **entrada** (a tarefa está pronta para começar?). A DoD é o portão de **saída** (a tarefa está realmente concluída?). As duas são checklists que padronizam o fluxo e reduzem riscos.

| | Definition of Ready (DoR) | Definition of Done (DoD) |
|---|---|---|
| Quando | **Antes** de iniciar a tarefa | Para **considerar concluída** |
| Garante | Informação disponível, requisito claro e compreendido | Qualidade e funcionalidade atendidas |
| Critérios típicos | Descrição clara, critérios de aceitação, dependências identificadas | Qualidade de código, testes unitários e de aceitação, code review, documentação atualizada, aprovação do PO |
| Evita | Mal-entendido e retrabalho | Entrega que "funciona" mas quebra a qualidade do produto |

## O exemplo do curso: fecha o ciclo das aulas 7 e 8
**DoR**
- [ ] Documentação de requisitos escrita, com o fluxo da solução ([[DDD 07 - Levantamento de requisitos|aula 7]])
- [ ] Refinamento técnico feito ([[DDD 08 - Refinamento técnico|aula 8]])
- [ ] Arquitetura da solução desenhada
- [ ] Quebrado em itens de desenvolvimento
- [ ] Estimado
- [ ] Priorizado pelo PM ou PO

**DoD**
- [ ] Code review
- [ ] Aprovado pela QA
- [ ] Validado com o usuário final
