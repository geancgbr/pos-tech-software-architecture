---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 3
fonte: "Aula 03- Descoberta e formação do conhecimento.pdf"
---

# DDD 03 - Descoberta e formação do conhecimento

← [[DDD 02 - Domain Storytelling]] · [[Domain Driven Design]] · Próxima → [[DDD 04 - Trabalhando com contextos delimitados]]

> [!summary] Em uma frase
> Para modelar o domínio é preciso entender o desafio do negócio, criar uma [[Linguagem Ubíqua]] e mantê-la documentada. É ela que ajuda a traçar os limites da solução, os [[Contexto Delimitado|Contextos Delimitados]].

## O desafio do negócio
- O que o negócio faz, quais são os processos e quais desafios já se conhecem. Só listar o óbvio não basta.
- A comunicação é uma **via de mão dupla**: o expert precisa falar de um jeito que o dev entenda, e o dev de um jeito que o expert entenda.
- Recorte da aula: **entrega e correção de atividades** na escola, porque usar a escola inteira deixaria o exemplo grande demais.

## Linguagem ubíqua
- É a linguagem com a terminologia **real do negócio**, usada pelo negócio e pelo time, e depois no próprio desenho do sistema.
- Exemplo da aula: os **pais** de uma criança que ainda está escolhendo escola são vistos de formas diferentes pela admissão, pelo marketing e pela secretaria.
- Ela deve ser **consistente e detalhada**. Dois cuidados no mapeamento: **termos ambíguos** e **termos sinônimos** (detalhes e uma ressalva em [[Linguagem Ubíqua]]).

## Modelagem do domínio
- O modelo é uma **abstração** do processo cujo problema queremos resolver. Ele conduz as conversas com os experts.
- É refinado a cada iteração, aplicando a ideia de realidade vs. desejo da [[DDD 02 - Domain Storytelling|aula 2]].

## Ferramentas: a wiki do projeto
Não existe fórmula mágica. Uma estrutura simples ajuda muito:
- uma wiki como central do projeto, com a descrição e o(s) time(s);
- **uma página por subdomínio**;
- uma seção de **linguagem ubíqua**, que funciona como dicionário;
- uma seção de **cenários**, com premissas e limitações;
- links para o repositório (código e documentação) e para a ferramenta de gestão.

Mantenha tudo atualizado a cada interação.

## Contextos delimitados (introdução)
- São **limites que impomos ao modelo**. Dentro de cada limite, termos, propriedades e operações compartilham uma única linguagem ubíqua.
- **Esses limites não vêm dos subdomínios**: eles saem da análise do negócio.
- Mais detalhes em [[Contexto Delimitado]]. Os pontos-chave:
  - não há regra de tamanho, e a linguagem ubíqua é a melhor métrica;
  - **um contexto pertence a um único time**, mas um time pode cuidar de vários contextos.
