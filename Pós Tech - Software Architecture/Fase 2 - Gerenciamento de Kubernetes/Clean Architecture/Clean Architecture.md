---
tags: [pos-tech/fase-2, clean-architecture, indice]
disciplina: Clean Architecture
fase: 2
aulas: 8
professor: Erick Muller
---

# Clean Architecture

[[Fase 2 - Gerenciamento de Kubernetes]] · Revisão → [[Revisão - Clean Architecture]]

Professor: **Erick Muller**. Os PDFs não têm título por aula ("Aula 01" a "Aula 08"); os nomes das notas abaixo são descritivos, criados a partir do conteúdo.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[CA 01 - Introdução e SOLID]] | [[SOLID]], [[Clean Architecture (livro)]] |
| 2 | [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]] | [[Arquitetura Hexagonal]], [[Entidade]], [[Casos de Uso]] |
| 3 | [[CA 03 - Camada de entidades]] | [[Entidade]], [[Linguagem Ubíqua]] |
| 4 | [[CA 04 - Camada de casos de uso]] | [[Casos de Uso]], [[Mock]] |
| 5 | [[CA 05 - Adaptadores de interface e frameworks e drivers]] | [[Controllers, Presenters e Gateways]], [[Detalhes na Arquitetura Limpa]] |
| 6 | [[CA 06 - Componentes]] | [[Componentes de Software]], [[Arquitetura Monolítica]] |
| 7 | [[CA 07 - Detalhes - dados, acesso e frameworks]] | [[Detalhes na Arquitetura Limpa]], [[Backend for Frontend (BFF)]] |
| 8 | [[CA 08 - Revisão da disciplina]] | [[SOLID]], [[Camadas da Arquitetura Limpa]] |

## A arquitetura em um quadro
| Camada (de dentro para fora) | Aula | O que é |
|---|---|---|
| Entidades | 2, 3 | Elementos de negócio e suas regras de consistência |
| Casos de Uso | 2, 4 | Uma regra de negócio por componente |
| Adaptadores de Interface | 5, 8 | Controllers, Presenters (ou Adapters) e Gateways |
| Frameworks e Drivers | 5, 7, 8 | O mundo exterior, tratado como "detalhe" |

Visão completa: [[Camadas da Arquitetura Limpa]]

## Divergências dentro da apostila
- **Presenters × Adapters**: na aula 5, os componentes dos Adaptadores de Interface são Controllers, **Presenters** e Gateways; na aula 8, Controllers, Gateways e **Adapters** (com o mesmo papel do Presenter).
- **"O que" × "como"**: na aula 4, um trecho diz que os casos de uso definem o "como", mas o resumo da aula 4 isola "o que" o software faz com os casos de uso e as entidades, a aula 3 trata as camadas internas (Casos de Uso e Entidades) como o "o que", e a aula 7 chama de "quê" os componentes das regras de negócio que entregam as funcionalidades.

## Ligações com a Fase 1
- [[Clean Architecture (livro)]] (Arquitetura de Software, aula 1) e [[Arquitetura Hexagonal]] (aula 5).
- [[Entidade]] e [[Linguagem Ubíqua]] (DDD).
- [[Mock]] e [[Teste de Integração]] (Qualidade de Software).

## Material
PDFs em `~/Desktop/Clean Architecture/`. **As notas resumem apenas o conteúdo escrito nos PDFs.** O código das aulas 2, 5 e 7 foi transcrito do PDF. O das aulas 3 e 4 está em imagem e não aparece nas notas, assim como os diagramas: quando uma nota cita uma figura, consulte o PDF.

## Referências
Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008) · Martin, *The Clean Coder* (2011) · Evans, *Domain-Driven Design* (2003) · Fowler, *UseCase* · *The Architecture of Open-Source Applications* · *Clean Code e Solid* (YouTube, 2021)
