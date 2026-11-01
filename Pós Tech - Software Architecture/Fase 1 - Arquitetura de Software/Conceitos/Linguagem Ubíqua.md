---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Ubiquitous Language, Linguagem Onipresente]
---

# Linguagem Ubíqua

A linguagem com a **terminologia real do negócio**, compartilhada por negócio e time e usada depois no desenho do sistema. Deve ser **consistente e detalhada**. Vale **dentro de um [[Contexto Delimitado]]**, e é justamente ela que ajuda a traçar esses limites.

Exemplo: "pais" significa coisas diferentes para admissão, marketing e secretaria. São três contextos, cada um com seu significado.

## Armadilhas no mapeamento
- **Termos ambíguos**: dentro de um subdomínio, um mesmo termo com vários significados. Exemplo: *política*, que pode ser lei regulatória ou regra interna da escola. A apostila diz que, como a linguagem ubíqua precisa de uma definição para cada termo, aqui se pode definir que *política* será usado para os dois significados.
- **Termos sinônimos**: dentro de um subdomínio, um termo usado para vários significados com muito mais detalhes. Exemplo: em TI, *login* é usado tanto para o ato de autenticar quanto para a conta do usuário, coisas totalmente diferentes com o mesmo nome por conveniência. Sempre que possível, **quebre esses termos e dê a eles definições únicas e específicas**.

## Na disciplina Arquitetura de Software (aula 2)
Também chamada de **linguagem onipresente**. É uma técnica de modelagem que adota uma linguagem **comum, clara e consistente**, entendida por todos os envolvidos (desenvolvedores, usuários, clientes e outras partes interessadas).
- Define os conceitos e termos importantes para o negócio e para o software, para que todos "falem a mesma língua".
- É útil principalmente em projetos com muitas partes interessadas e complexidade significativa.
- Costuma ser usada junto com outras técnicas, como a modelagem de domínio.
- Reduz mal-entendidos e ajuda o software a atender aos requisitos e às expectativas.
- Muitos analistas deixam de registrá-la, mas ela ajuda quando é preciso voltar a conversar com os stakeholders. → [[ARQ 02 - Processo e modularização]], [[QS 05 - Trabalhando com BDD]]

## Na disciplina Qualidade de Software (aula 5)
É um dos princípios do [[BDD (Behavior-Driven Development)|BDD]]: usar uma linguagem de domínio comum, para que todos falem a mesma língua. A linguagem dos cenários e dos testes deve ser compreensível por devs, usuários e partes interessadas. → [[QS 05 - Trabalhando com BDD]]

## Na disciplina Clean Architecture (Fase 2)
As **entidades** recebem os nomes do negócio, com base na linguagem ubíqua do DDD: a linguagem da regra de negócio e do cliente, não a da implementação (TypeScript, C#, Java). Nomes incomuns levam a entidades desconectadas da realidade. → [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]], [[CA 03 - Camada de entidades]]

## Onde manter
Um dicionário numa wiki ou ferramenta como o Notion, **sempre atualizado**. Veja a estrutura de wiki em [[DDD 03 - Descoberta e formação do conhecimento#Ferramentas: a wiki do projeto]].

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
O DDD enfatiza uma **linguagem comum** entre devs e stakeholders, fundamental com serviços mantidos por **equipes diferentes** ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]). O **high-level domain model** ajuda a criar essa linguagem para toda a organização ([[MS2 01 - Desenhando a lógica de negócios com microsserviços]]).

Aparece em: [[DDD 03 - Descoberta e formação do conhecimento]], [[ARQ 02 - Processo e modularização]], [[QS 05 - Trabalhando com BDD]], [[MS2 01 - Desenhando a lógica de negócios com microsserviços]], [[MS2 02 - Aplicando a lógica de negócios no microsserviço]]
