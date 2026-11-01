---
tags: [pos-tech/fase-1, arquitetura, aula]
disciplina: Arquitetura de Software
aula: 2
fonte: "Aula 2 - Arquitetura de Software_revFinal.pdf"
---

# ARQ 02 - Processo e modularização

← [[ARQ 01 - Introdução à arquitetura de software]] · [[Arquitetura de Software]] · Próxima → [[ARQ 03 - Documentação, testabilidade e modificabilidade]]

> [!summary] Em uma frase
> Os primeiros passos de uma boa arquitetura vão do [[Processo de Desenvolvimento de Software|levantamento de requisitos]] (com a [[Modelagem Tática|modelagem tática]] e a [[Linguagem Ubíqua|linguagem ubíqua]]) até a [[Modularização|modularização]] do sistema.

## Hands On (vídeos)
**Simulação de levantamento de requisitos**: o professor Kaku faz o papel de analista e o professor Thiago, de stakeholder.

**Perguntas do analista**
- Quais são as principais funcionalidades do sistema?
- Depois dessa etapa, qual seria a próxima?
- Quais bugs o sistema traz que mais travam vocês?

**Falas do stakeholder** (o PDF lista separado das perguntas)
- A principal funcionalidade é cortar um vídeo **em tempo real**: aconteceu algo agora, e o vídeo precisa estar no sistema para ser editado e publicado nas redes sociais dos veículos.
- Escolher as redes sociais das editorias ligadas ao vídeo. Exemplo: um acidente vai para o Brasil Urgente; entretenimento pode ir para outro canal.
- Às vezes o sistema cai e eles perdem tudo o que estavam fazendo, sendo levados à tela de login.

- O professor mostra um print da primeira versão do **REC** e formas de dividir o código em módulos usando **C#**.
- Quebra de módulos da nova versão do REC (Figura 1 do PDF): **Usuários** (com gerenciamento de perfil), **Canais** (com gerenciamento) e **Redes sociais** (compartilhamento de conteúdo).

## Processo de desenvolvimento de software
- É uma abordagem **sistemática e disciplinada**, que visa garantir **qualidade, eficiência e eficácia**.
- **Etapas**: análise de requisitos, design, implementação, testes e manutenção.
- Para quem trabalha com DDD, esta etapa seria a **modelagem tática**: entrevistar clientes e stakeholders (quem conhece o negócio) para levantar todos os requisitos.
- O analista precisa ter em mente as **regras de negócio**, com foco em tudo o que o sistema precisa ter para existir, porque esses detalhes são cruciais para a arquitetura.
- Um ponto que muitos analistas deixam de registrar é a **linguagem ubíqua**, que ajuda no decorrer do desenvolvimento, quando é preciso voltar a conversar com os stakeholders.

## Resumo de DDD dado nesta aula
- **[[Modelagem Tática]]**: processo de análise e planejamento que define ações específicas para alcançar objetivos operacionais e estratégicos. As equipes criam planos detalhados para metas de curto e médio prazo.
- **[[Linguagem Ubíqua]]** (ou linguagem onipresente): linguagem comum, clara e consistente, entendida por todos os envolvidos (desenvolvedores, usuários, clientes e outras partes interessadas).
- Leitura complementar indicada: *Implementando Domain-Driven Design*, de Vaughn Vernon.

> [!warning] Mesmo termo, sentidos diferentes nas apostilas
> Aqui, "modelagem tática" é o levantamento de requisitos e o planejamento de ações de curto e médio prazo. Na disciplina de DDD, "[[Design Tático]]" é o "como": camadas, entidades, objetos de valor, agregados.

## Modularização
- O sistema é dividido em **módulos independentes**, cada um com uma função específica, que podem ser desenvolvidos, testados e mantidos separadamente.
- **Vantagens**: mais fácil de entender, de modificar e de atualizar; mais flexível (novos módulos entram sem afetar o resto); melhor qualidade (erros detectados e corrigidos por módulo); desenvolvimento mais eficiente (equipes em módulos diferentes ao mesmo tempo).
- **Cuidados**: as interfaces entre módulos precisam ser **claras e bem definidas**, e a organização dos módulos precisa ser lógica e coerente.
- **Exemplo**: num comércio eletrônico, há um módulo de pedidos, um de pagamentos e um de estoque. O módulo de pagamentos consulta o de pedidos para saber se um pedido foi pago antes de marcá-lo como "processado".

Detalhes em [[Modularização]].

## Referências
Evans, *Domain-Driven Design* (Alta Books, 2016) · Vernon, *Implementando Domain-Driven Design* (Alta Books, 2013)
