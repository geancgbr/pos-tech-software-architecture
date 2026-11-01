---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 5
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 5.pdf"
---

# DOC 05 - Architecture Decision Records (ADRs)

← [[DOC 04 - Requisitos funcionais e não funcionais]] · [[Documentação de Arquitetura de Soluções]] · Próxima → [[DOC 06 - DAS (Design Approval Sheet)]]

> [!summary] Em uma frase
> Uma [[ADR (Architecture Decision Record)|ADR]] registra **uma decisão significativa de arquitetura**, com o contexto e os motivos ("o porquê"). Tem estado e ciclo de vida, e **fica imutável depois de aceita**. O conjunto das ADRs forma o **log de decisões** do projeto.

## Hands On (vídeos)
Criação e documentação de ADRs em situações reais, do contexto à análise das alternativas.

## O que é e por que usar
- Documenta as decisões de arquitetura com o **contexto e as razões**, formando um histórico de como a arquitetura evoluiu.
- **Problema que resolve**: em projetos longos, decisões se perdem ou ficam mal documentadas, e equipes futuras não entendem por que algo foi escolhido. Isso gera inconsistência e retrabalho.
- **Benefícios**:
  - comunicação entre devs, arquitetos e stakeholders;
  - **preservação do conhecimento** e continuidade (novos membros entendem rápido);
  - **adaptabilidade**: revisitar decisões quando requisitos e prioridades mudam;
  - **governança de tecnologia**.

## Estrutura e ciclo de vida
- Cada ADR tem **decisão, contexto e consequências**, um **estado** e um **ciclo de vida**. O conjunto delas forma o **log de decisões**.
- Os membros podem ler **só os títulos**, para ter o contexto rápido, ou ler em detalhe.
- O mínimo de cada ADR é **contexto, decisão e consequências**. O foco está nos **motivos**, não na implementação. Entender o "porquê" facilita a adoção e evita que arquitetos futuros invalidem decisões já acordadas.

**Escopo: crie uma ADR para decisões que afetem**
- a estrutura do sistema (ex.: microsserviços);
- os requisitos não funcionais (ex.: segurança, alta disponibilidade);
- as dependências entre componentes;
- as interfaces (APIs, contratos);
- as técnicas de construção (bibliotecas, ferramentas, processos).

Essas decisões costumam ser guiadas por [[Requisitos Funcionais e Não Funcionais|requisitos funcionais e não funcionais]].

**Processo** (Figura 1 do PDF)
1. Alguém identifica a necessidade e começa a escrever, usando um **modelo padrão**.
2. Define-se um **"dono(a)"**, que mantém e comunica a ADR. Qualquer membro pode criar e sugerir mudanças, mas o dono aprova as alterações.
3. A ADR entra no estado **"Proposto"**, e o dono conduz a **revisão** com a equipe em reunião (leitura, comentários, dúvidas).
4. Se precisar de mudanças, continua "Proposto" e o dono define as ações antes de uma nova revisão. Se for **rejeitada**, o motivo é registrado, para evitar discussões futuras. Se for **aprovada**, vira **"Aceito"**.
5. Depois de aceita, é **imutável**. Para mudar, cria-se uma **nova ADR**, e a anterior recebe o estado **"Superada"**.

As ADRs servem de **referência em code reviews** e revisões de arquitetura: os revisores verificam se as mudanças estão alinhadas com elas.

## As seções
**As 4 seções principais** (estrutura "amplamente aceita na indústria")

| Seção | Conteúdo |
|---|---|
| **Contexto** | O problema, as restrições e os fatores que influenciam a decisão. Claro e completo, para entender o cenário no futuro |
| **Decisão** | A escolha, como será implementada, por que foi escolhida e as implicações |
| **Consequências** | Benefícios, limitações e desafios, para antecipar ajustes e gerenciar riscos |
| **Alternativas** | Outras opções consideradas e por que foram descartadas, para evitar discussões futuras |

**"Como implementar uma ADR"** (Quadro 1 do PDF)
- **Título**: curto e descritivo.
- **Data**: dd/mm/yyyy.
- **Status**: Proposta · Aceita · Depreciada (não faz mais sentido) · Substituída (por outra) · Rejeitada.
- **Contexto**: as considerações e forças (tecnológicas, políticas, econômicas, sociais, do projeto).
- **Decisão**: em **voz ativa**, frases completas, em parágrafos.
- **Consequências**: positivas e negativas; tudo o que possa afetar o time e o projeto.

> [!warning] Diferenças entre os trechos da apostila
> - **Seções**: na aula 1, o formato padrão é "decisão, contexto, status e consequências". Na aula 5, as 4 seções principais são **Contexto, Decisão, Consequências e Alternativas**, e o quadro de implementação tem Título, Data, Status, Contexto, Decisão e Consequências.
> - **Nomes dos estados**: o texto do processo usa Proposto, Aceito, Rejeitado e **Superada**. O quadro usa Proposta, Aceita, **Depreciada**, **Substituída** e Rejeitada.

O exemplo prático de ADR (escolha de um mecanismo de busca) está na Figura 2 do PDF (Skalena).

## Quando usar e quando não usar
**Use** para decisões que **impactam diretamente a arquitetura** e são **difíceis de reverter**: frameworks, tecnologias críticas, mudanças em componentes centrais. Exemplo: **microsserviços × monolito**, com os motivos (escalabilidade, complexidade), para reavaliar as premissas depois.

**Não use**
- Decisões **triviais ou temporárias**: ajustes temporários de configuração, atualização de uma dependência menor. Para isso servem os **changelogs** ou o versionamento.
- **Prototipagem** e iterações rápidas: o excesso gera **"dívida de documentação"**.

## Vantagens e riscos
**Vantagens**: menor curva de aprendizado para quem chega · **centralização** num repositório acessível, o que melhora a governança e evita redundâncias e conflitos.

**Sem ADRs**:
- o "porquê" se perde, o que é grave em projetos longos ou com alta rotatividade;
- surgem **decisões conflitantes** (ex.: duas equipes escolhendo métodos de autenticação diferentes, o que gera complexidade desnecessária);
- decisões são revertidas sem análise crítica, gerando retrabalho e **débito técnico**.

## Boas práticas
- Clara e concisa, focada no essencial.
- **Repositório centralizado**, com pastas por tema ou componente.
- Ao registrar as razões, as ADRs reduzem o débito técnico, aumentam a transparência e promovem uma cultura de responsabilidade. Cada decisão pode ser revisada e questionada.

## Referências
AWS, *ADR Process (Prescriptive Guidance)* (2022) · Henderson, *Architecture Decision Record* (adr.github.io, 2017) · Microsoft, *Architecture Decision Record* (2023) · Skalena, *Um guia sobre ADR* (2023) · Zup, *Architecture Decision Records* (2021)
