---
tags: [pos-tech/fase-1, arquitetura, indice]
disciplina: Arquitetura de Software
fase: 1
aulas: 5
---

# Arquitetura de Software

[[Fase 1 - Arquitetura de Software]] · Revisão → [[Revisão - Arquitetura de Software]]

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[ARQ 01 - Introdução à arquitetura de software]] | [[O que é Arquitetura de Software]], [[Clean Architecture (livro)]], [[Design Patterns]], [[Arquitetura de Camadas]] |
| 2 | [[ARQ 02 - Processo e modularização]] | [[Processo de Desenvolvimento de Software]], [[Modelagem Tática]], [[Linguagem Ubíqua]], [[Modularização]] |
| 3 | [[ARQ 03 - Documentação, testabilidade e modificabilidade]] | [[Documentação de Software]], [[Testabilidade]], [[Modificabilidade]] |
| 4 | [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]] | [[Escalabilidade]], [[Disponibilidade e Observabilidade]], [[Desempenho]], [[Estratégias de Cache]] |
| 5 | [[ARQ 05 - Arquitetura Hexagonal]] | [[Separação de Conceitos (SoC)]], [[Arquitetura Hexagonal]], [[Portas e Adaptadores]], [[Atores Condutores e Conduzidos]], [[Inversão de Controle (IoC)]] |

## Termos que mudam de sentido entre as disciplinas
| Termo | Arquitetura de Software | Domain Driven Design |
|---|---|---|
| Camada de **aplicação** | Contém a lógica de negócios ([[Arquitetura de Camadas]]). Na hexagonal, o "Application" do centro é o domínio e não tem relação com a camada de aplicação | **Não** contém regra de negócio ([[Camadas do DDD]]) |
| **Tático** | [[Modelagem Tática]]: levantar requisitos e planejar ações de curto e médio prazo | [[Design Tático]]: o "como" (camadas, entidades, VOs, agregados) |

## Lab prático
[ddd-hexagonal](https://github.com/geancgbr/ddd-hexagonal): API de pedidos em Java com Objetos de Valor, Entidades, Agregado, Serviço de Domínio, Eventos de Domínio e Portas e Adaptadores. É código meu para praticar, não conteúdo da apostila.

## Material
PDFs em `~/Desktop/FASE 1/Arquitetura de Software/`. **As notas resumem apenas o conteúdo escrito nos PDFs.** As figuras (módulos do REC, fluxo de cache, pirâmide de testes, desenho original do hexágono, atores) não estão nas notas: quando uma nota cita uma figura, consulte o PDF. Os itens de "Hands On" resumem o que o PDF diz que foi mostrado nos vídeos.

## Referências
Bass, Clements e Kazman (2012) · Evans (2016) · Vernon (2013) · Aniche (2013, 2015) · Vazquez e Simões (2016) · Fowler, S. J. (2017) · Majors, Fong-Jones e Miranda (2022) · Branas (2022) · Valente (2020) · Shrivastava e Srivastav (2022)
