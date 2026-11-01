---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 2
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 2.pdf"
---

# DOC 02 - High-Level Design (HLD) e Low-Level Design (LLD)

← [[DOC 01 - Introdução à documentação de arquitetura]] · [[Documentação de Arquitetura de Soluções]] · Próxima → [[DOC 03 - Modelos e diagramas de arquitetura - C4 Model]]

> [!summary] Em uma frase
> O [[HLD e LLD (High-Level Design e Low-Level Design)|HLD]] dá a **visão macro** e alinha o time com os stakeholders. O **LLD** entra nos **detalhes técnicos** para a implementação. São documentos **complementares**: o HLD vem primeiro e o LLD em seguida.

## Hands On (vídeos)
HLD e LLD: por que são importantes, como usá-los, melhores práticas e dicas para deixar a documentação mais clara.

## HLD × LLD
| | High-Level Design (HLD) | Low-Level Design (LLD) |
|---|---|---|
| Visão | **Macro**: componentes principais, relações, arquitetura geral | **Detalhada**: cada componente com especificações e instruções de implementação |
| Para quê | Alinhar o time com os **stakeholders**; ponte de comunicação entre a equipe técnica e os stakeholders | Guiar a **implementação técnica** pela equipe de desenvolvimento |
| Linguagem | Simplificada, com diagramas visuais | Técnica: classes, métodos, especificações |
| Nível de detalhe | Alto nível. Ex.: como os servidores interagem com os bancos, ou como a rede suporta a comunicação entre módulos | Especifica **nomes de serviços, tecnologias e até linguagens ou fornecedores** |
| Quando | **Primeiro** | **Em seguida**, detalhando cada componente |
| Exemplos de figura no PDF | Componentes de um HLD (Figura 1) | Diagrama de sequência (Figura 2), fluxograma de e-commerce (Figura 3), arquitetura AWS de web hosting (Figura 4) |

## High-Level Design
- **Visão macro** de como as partes maiores se integram para atender aos requisitos e objetivos.
- **Ponte de comunicação**: os stakeholders entendem o escopo e as funcionalidades sem aspectos técnicos complexos, o que reduz mal-entendidos.
- **Gerencia expectativas** e **valida a direção** do projeto antes do detalhamento: ajustes logo no início otimizam tempo e recursos e minimizam riscos.
- **Elementos de um HLD eficaz**: **visão geral** do sistema (objetivo, principais funcionalidades), **diagrama de arquitetura** (componentes-chave e interações) e **lista de requisitos de alto nível**. A estrutura pode variar, mas o essencial permanece.
- **Componentes**: os blocos de construção do sistema (sistemas, tecnologias e outros componentes essenciais), descritos em alto nível.
- **Sem HLD**: interpretações divergentes, retrabalho, desperdício, incompatibilidades, atrasos e custos maiores.
- **Como criar**: definir a estrutura básica; descrever os elementos com clareza, sem detalhes excessivos; incluir **só os aspectos mais críticos**; **validar com a equipe técnica e os stakeholders**.

## Low-Level Design
- **Próximo passo após o HLD**. Cada componente é descrito minuciosamente: a funcionalidade e **como deve ser construído**.
- **Evita ambiguidades** e garante a consistência. É um guia técnico para os devs.
- **Estrutura**: fluxos de dados, algoritmos, especificações de interfaces e diagramas técnicos como **fluxogramas** (o fluxo de um processo) e **diagramas de sequência** (a interação entre componentes).
- **Benefícios**: compreensão completa, implementação correta, identificação de problemas, manutenção mais fácil. Serve de referência para atualizações futuras e reduz erros.

## Juntos
- Complementares, usados em etapas diferentes do ciclo.
- **Boa prática**: revisar e atualizar os dois constantemente para refletir as mudanças no projeto.

## Mercado, cases e tendências
Leitura recomendada: *Fundamentos da Arquitetura de Software: uma Abordagem de Engenharia*, de Mark Richards.

## Referências
HyScaler, *HLD vs LLD in SDLC* (2024) · GeeksforGeeks, *Difference between HLD and LLD* (2024) · NetSec Cloud, *High-Level vs. Low-Level Design* (2024)
