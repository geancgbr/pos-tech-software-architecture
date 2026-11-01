---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 6
fonte: "Aula 6.pdf (Erick Muller)"
---

# CA 06 - Componentes

← [[CA 05 - Adaptadores de interface e frameworks e drivers]] · [[Clean Architecture]] · Próxima → [[CA 07 - Detalhes - dados, acesso e frameworks]]

> [!summary] Em uma frase
> [[Componentes de Software|Componentes]] são unidades de código com **responsabilidade bem definida** e **interfaces de uso claras**, que se combinam para resolver problemas complexos, em vez de um grande [[Arquitetura Monolítica|monolito]]. Regras: **responsabilidade mínima**, sem sobreposição, composição, e adaptar a ferramenta ao problema (nunca o contrário).

## Hands On (vídeos)
Componentizar uma solução criada como um grande bloco de código, entendendo como isso deixa mais claros os limites e as responsabilidades do software.

## Foco da aula
Aqui não se pensa em código nem em implementação, e sim no **processo de detalhar a solução com componentes de arquitetura**. Mesmo considerando as restrições tecnológicas (plataforma, linguagem, integrações obrigatórias), ver a arquitetura como **desenho da organização interna do produto** ajuda a tomar decisões melhores.

## O que são componentes
- **Unidades de código com responsabilidade bem definida**, agrupadas e organizadas para resolver problemas.
- **"Responsabilidade bem definida"** quer dizer fazer coisas simples com **total competência**. Um componente de acesso a banco precisa fazer **toda** a comunicação; implementar só uma parte serve para menos situações.
- **Interfaces de uso bem definidas**: no componente de SGBD, "abrir conexão", "rodar comando" e "rodar pesquisa" precisam ser **explícitas** (o nome corresponde à operação) e simples de usar. Se não forem, o componente não é usado, porque causa mais problemas do que resolve.
- Conectar componentes pelas interfaces permite construir **soluções complexas a partir de componentes menos complexos**, em vez de um grande monolito.

## Arquitetura monolítica
- **Centraliza numa única unidade de código todas as responsabilidades** (interface, acesso a recursos externos, regras de negócio, configurações): um "super software" altamente integrado.
- **Não é intrinsecamente ruim**. É adequada para soluções **pequenas**, com poucas interfaces ou um caso de uso muito específico, como **software embarcado em micro ou nanodispositivos**.
- **Vira problema** quando junta várias responsabilidades num componente, ou delega a poucos componentes muito especializados e tudo acaba centralizado. A manutenção fica difícil, e o **custo cresce com o tempo de vida** da solução.

Veja [[Arquitetura Monolítica]].

## Componentização e responsabilidade
- Cada pedaço é especializado e preparado para trabalhar dentro de algo maior, como a **peça de um carro**: funcional sozinha, útil só quando conectada.
- **Regra da responsabilidade mínima**: implementar o **mínimo possível para ser útil** num contexto. O que sobrar vai para outro componente, e nada deve ficar incompleto.
- **Exemplo**: a classe Estudante é **útil** (limites e responsabilidade bem definidos) e **competente** (campos para caracterizá-la de forma inequívoca e validação). Herdando de Pessoa, a responsabilidade fica isolada: o contexto de Estudante é diferente do de Pessoa, possivelmente uma extensão dela.

## Reutilização, bibliotecas, repositórios, frameworks e código aberto
- Use a **quantidade adequada** de componentes, nem todos só porque existem.
- **Reutilização**: um componente bem isolado e desacoplado (ex.: conexão com uma API) pode ir para outro projeto. Algumas organizações têm **repositórios de componentes** testados e aprovados.
- **Bibliotecas** agrupam componentes por contexto de uso. Você baixa a biblioteca inteira, mas usa só o necessário.
- **git, github.com, gitlab.com** permitiram compartilhar desde pequenos trechos até componentes completos, abertos e adaptáveis. Os toolkits das linguagens trazem gerenciadores como o **npm** (JavaScript/TypeScript) e o **pip** (Python).
- **Framework**: uma estrutura de código para agilizar a construção de componentes, **como uma casa pré-fabricada**, com uma base conhecida e testada. O uso principal é em **APIs RESTful**, com referências como o **Spring** (Java) e o **Express** (JavaScript).
- A maioria é gratuita, sob licenças de código aberto. Construir uma arquitetura hoje envolve decidir **o que construir, o que reutilizar da organização e o que aproveitar de uso livre**.

## Conceitos para decidir melhor
Não há receita automática, mas há conceitos que ajudam:

| Conceito | Ideia |
|---|---|
| **Isolamento de responsabilidade** | A pergunta "o que isto deve fazer?". **Cada componente com sua responsabilidade, sem sobrepor nem compartilhar**: se dois fazem a mesma coisa, qual usar? Isso não pode existir na Arquitetura Limpa |
| **Composição e desacoplamento** | Isolar para poder **combinar**, como numa máquina. Exemplo: um componente de acesso a dados composto de três (acesso ao banco, entidades e adaptação dos dados para entidades). Internamente é acoplado, mas fica **desacoplado do resto** do sistema, e ainda dá para injetar nele outro componente de acesso a dados |
| **Usar o mínimo** | O mínimo necessário, e sempre que possível **compor** componentes existentes, já reconhecidos como seguros, para novos comportamentos |
| **Adaptar a ferramenta à necessidade** | **Um dos maiores erros** é adaptar a arquitetura aos componentes: escolher componentes familiares e depois "entortar" a arquitetura para caber neles, o que gera **débito técnico**. O certo é desenhar a arquitetura básica, entender o problema e **só depois** escolher os componentes. Exemplo: escolher um framework antes de saber se ele é necessário; o código de adaptação muitas vezes é maior que o da solução |
| **Conhecer arquiteturas diferentes** | **Praticando** (faça, teste, analise e melhore, num pensamento ágil) e **estudando**: ler código de projetos abertos e entender as decisões. Só a experiência produz uma arquitetura de alta qualidade |

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008) · *The Architecture of Open-Source Applications* (aosabook.org) · Fowler, *UseCase*
