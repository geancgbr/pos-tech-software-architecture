---
tags: [pos-tech/fase-1, documentacao, conceito]
aliases: [HLD, LLD, High-Level Design, Low-Level Design, Design de alto nível, Design de baixo nível]
---

# HLD e LLD (High-Level Design e Low-Level Design)

Documentos **complementares**. O **HLD** é criado **primeiro**, e o **LLD** vem **em seguida**.

| | HLD | LLD |
|---|---|---|
| Visão | **Macro**: estrutura global, componentes principais e como se interconectam (módulos, sistemas externos, padrões de comunicação) | **Detalhada**: cada componente, com estrutura interna (classes, métodos, algoritmos, fluxos de dados, interações) |
| Público e papel | Alinhar a equipe com os **stakeholders**; ponte de comunicação entre a equipe técnica e os stakeholders; gerenciar expectativas e validar a direção | Guiar a **implementação**; verificar a conformidade do código |
| Detalhe | **Sem detalhar a implementação** | Especifica nomes de serviços, tecnologias, linguagens, fornecedores |
| Contém | Visão geral, diagrama de arquitetura, lista de requisitos de alto nível | Fluxos de dados, algoritmos, especificações de interfaces, fluxogramas, diagramas de sequência e de classes |
| Boas práticas | Só os aspectos críticos; claro e conciso; validar com o time e os stakeholders; incluir diagramas de interação | Organizado logicamente; incluir padrões e restrições técnicas; atualizar em ciclos ágeis |

Os dois devem ser **revisados e atualizados constantemente**.

O [[C4 Model]] faz a **transição gradual** entre os dois: o nível de Contexto é comparável ao HLD, e o de Contêiner é intermediário.

Aparece em: [[DOC 01 - Introdução à documentação de arquitetura]], [[DOC 02 - High-Level Design (HLD) e Low-Level Design (LLD)]], [[DOC 03 - Modelos e diagramas de arquitetura - C4 Model]]
