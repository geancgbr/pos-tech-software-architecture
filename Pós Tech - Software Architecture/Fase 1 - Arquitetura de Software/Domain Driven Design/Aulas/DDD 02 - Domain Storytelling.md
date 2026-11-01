---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 2
fonte: "Aula 02- Domain Storytelling.pdf"
---

# DDD 02 - Domain Storytelling

← [[DDD 01 - Introdução ao Domain-Driven Design]] · [[Domain Driven Design]] · Próxima → [[DDD 03 - Descoberta e formação do conhecimento]]

> [!summary] Em uma frase
> [[Domain Storytelling]] (Narrativa de Domínio) é uma técnica colaborativa: o [[Domain Expert]] conta a história do domínio e alguém a desenha numa linguagem de pictogramas (atores, objetos de trabalho e atividades numeradas).

## Por que contar histórias (Hofer & Schwentner)
Contar histórias ajuda a entender o domínio e a criar uma linguagem comum entre Domain Experts e IT Experts (o embrião da [[Linguagem Ubíqua]]). Também ajuda a evitar mal-entendidos, esclarecer requisitos, implementar e estruturar o software corretamente e desenhar processos de negócio viáveis.

## A linguagem pictográfica

| Elemento | O que é | Regras e dicas |
|---|---|---|
| **Ator** | Pessoa, grupo, objeto ou sistema que age na história | A história é contada do ponto de vista dele. Nomeie pela **função**, nunca pelo nome da pessoa |
| **Objeto de trabalho** | O que o ator usa: algo físico (ticket, menu), digital (ticket digital) ou uma interação (e-mail, ligação) | Os atores interagem com eles, e isso forma o fluxo |
| **Atividade** | Seta com o **verbo da ação** | **Sem condicionais (if/else)**: cada variação vira outra história. **Sem retornos (loopbacks)**: para isso existe BPMN |
| **Número sequencial** | Ordem das atividades | Ações em paralelo podem levar o mesmo número, mas use pouco. O expert conta fora de ordem, então ajuste a numeração |
| **Anotação** | Texto explicativo | Limitações, ações necessárias, gatilhos para outros processos |
| **Grupo** | Linha de limite em volta de parte da história | Ações repetidas, subdomínios, limitações |
| **Cor** | Destaque | Para dar ênfase a uma sequência de atividades |

Ferramenta usada nos exemplos: **egon.io**.

## Cenários e escopo
- **Cenário**: uma história tem um caminho principal e variações. Cada variação vira um novo cenário.
- **Escopo** tem começo, meio e fim, mas pode ter variações e limitações. Até onde ir com as histórias: segundo Cockburn (2001), o nível aceitável é o **nível do mar**, ou seja, objetivos do usuário, até o **nível da ostra**. Se você foi longe demais na história, isso não impede de aprofundar mais tarde.
- **Realidade vs. desejo**: o expert descreve o processo de hoje (**AS IS**), mas, ao contar, já começa a imaginar como deveria ser (**TO BE**). Separe as duas versões. O TO BE não precisa nascer pronto e pode ser entregue aos poucos.

## Equipe de trabalho
- **Domain Experts**: quantos forem necessários.
- **Ouvintes**: normalmente o time de desenvolvimento.
- **Moderador**: conduz as perguntas e mantém o foco.
- **Modelador**: desenha a história em pictogramas e faz as anotações.

## Relacionados
Na [[DDD 06 - Event Storming|aula 6]], o [[Event Storming]] é apresentado como "bem parecido" com o Domain Storytelling, também para compartilhar conhecimento do negócio e com uma equipe semelhante (lá o papel de condução se chama facilitador).
