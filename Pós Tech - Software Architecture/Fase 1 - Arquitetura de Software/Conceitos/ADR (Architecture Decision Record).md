---
tags: [pos-tech/fase-1, documentacao, conceito]
aliases: [ADR, ADRs, Architecture Decision Record, Architecture Decision Records, Registro de Decisão Arquitetural, Log de decisões]
---

# ADR (Architecture Decision Record)

**Registro de Decisão Arquitetural**: documenta uma **decisão significativa** de arquitetura com o **contexto e os motivos**. O conjunto das ADRs forma o **log de decisões**.

**Regras principais**
- Foco no **porquê**, não na implementação.
- Tem um **dono(a)**, que mantém, comunica e aprova as alterações.
- **Ciclo de vida**: Proposto → revisão em equipe → Aceito ou Rejeitado (o motivo é registrado).
- **Depois de aceita, é imutável**. Para mudar, cria-se uma nova ADR, e a anterior fica **Superada**.
- Serve de referência em **code reviews**.

**Seções**: **Contexto · Decisão · Consequências · Alternativas** (as 4 principais na aula 5). O quadro "Como implementar uma ADR" traz **Título, Data, Status, Contexto, Decisão e Consequências**. Alternativas não aparece no quadro.

**Status no quadro**: Proposta · Aceita · Depreciada · Substituída · Rejeitada.

> [!warning] As aulas usam nomes diferentes
> Na aula 1, o formato padrão é "decisão, contexto, status e consequências". O texto do processo na aula 5 usa os estados Proposto, Aceito, Rejeitado e **Superada**, enquanto o quadro usa **Depreciada** e **Substituída**.

**Quando criar**: decisões que afetam a estrutura do sistema, os RNF, as dependências, as interfaces (APIs e contratos) e as técnicas de construção, e que são **difíceis de reverter**. Exemplo: microsserviços × monolito.

**Quando não criar**: decisões triviais ou temporárias (use changelog ou versionamento) e prototipagem com iterações rápidas (risco de **"dívida de documentação"**).

**Sem ADRs**: o "porquê" se perde · surgem decisões conflitantes (ex.: dois métodos de autenticação) · decisões são revertidas sem análise, gerando **débito técnico**.

Template citado na aula 1: **Michael Nygard**. As ADRs também fazem parte do [[DAS (Design Approval Sheet)|DAS]].

Aparece em: [[DOC 01 - Introdução à documentação de arquitetura]], [[DOC 05 - Architecture Decision Records (ADRs)]], [[DOC 06 - DAS (Design Approval Sheet)]]
