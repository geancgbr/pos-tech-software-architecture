---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 1
fonte: "Aula 01- Introdução à Domain Driven Design.pdf"
---

# DDD 01 - Introdução ao Domain-Driven Design

[[Domain Driven Design]] · Próxima → [[DDD 02 - Domain Storytelling]]

> [!summary] Em uma frase
> O DDD serve para construir uma solução que fale a língua do negócio. Ele começa pelo [[Design Estratégico]]: entender o [[Domínio]], dividi-lo em [[Subdomínios]] e achar quem conhece o negócio ([[Domain Expert]]).

## Ideias principais
- **DDD não é metodologia de projeto.** É uma cultura de comunicação e documentação entre o time de desenvolvimento e o negócio. Veja [[O que é DDD]].
- O conhecimento do negócio **nunca está centralizado** (Vernon). O time precisa ouvir várias pessoas, com habilidades diferentes, para descobrir os requisitos funcionais e não funcionais. Isso orienta **o que** fazer, **por que** e **quando** (prioridade).
- **[[Design Estratégico]]** responde ao "o quê" e ao "por quê": saber aonde queremos chegar. O "como" ([[Design Tático]]) fica para a [[DDD 05 - Implementando arquitetura e lógica|aula 5]].
- **[[Domínio]]** é a área de atividade à qual o usuário aplica o programa. Pode ser física (pessoas embarcando num avião) ou intangível (dinheiro, na contabilidade). O domínio de uma escola é a **Educação**.
- **[[Subdomínios]]** são de três tipos: Principal, Genérico e Suporte.
- **[[Domain Expert]]** é quem detectou a necessidade e conhece o negócio a fundo; é quem "conta a história". Um domínio tem vários subdomínios e, portanto, vários Domain Experts.

## Exemplos da aula

| Empresa | Principal (diferencia) | Genérico (comum no mercado) | Suporte (apoia, geralmente CRUD) |
|---|---|---|---|
| Escola | Aulas e metodologias | Criptografia dos dados | Gestão de dados de pais e alunos |
| Netflix | Vídeos | Faturamento | Cadastro de filmes e séries |
| Azul | Voos | Autenticação do portal | Cadastro de pessoas no portal |
| DHL | Serviços logísticos | Contabilidade | Integração com outros sistemas logísticos |

## Para lembrar
- O tipo de um subdomínio **depende do negócio**: o que é genérico para uma empresa pode ser principal para outra.
- A **escola** é o cenário que acompanha a disciplina inteira.
- A apostila mostra um fluxograma para identificar o tipo de subdomínio (Figura 1, pág. 7 do PDF, fonte: vladikk.com). O texto do PDF não descreve as etapas do fluxograma, então consulte a figura no PDF.
