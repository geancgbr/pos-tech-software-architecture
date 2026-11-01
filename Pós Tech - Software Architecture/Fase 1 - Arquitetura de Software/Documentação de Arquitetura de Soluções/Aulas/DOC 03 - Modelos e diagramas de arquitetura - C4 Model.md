---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 3
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 3.pdf"
---

# DOC 03 - Modelos e diagramas de arquitetura: C4 Model

← [[DOC 02 - High-Level Design (HLD) e Low-Level Design (LLD)]] · [[Documentação de Arquitetura de Soluções]] · Próxima → [[DOC 04 - Requisitos funcionais e não funcionais]]

> [!summary] Em uma frase
> O [[C4 Model]], criado por **Simon Brown**, documenta a arquitetura em **4 níveis**, do macro ao micro: **Contexto, Contêiner, Componente e Código**. Cada público vê o nível de detalhe que importa para ele, numa transição gradual entre o HLD e o LLD.

## Hands On (vídeos)
O C4 Model no dia a dia, integrado a outros diagramas. Segundo o PDF, os vídeos também tratam do uso do C4 em **diagramas de Deployment**.

## A ideia
- Abordagem moderna e simplificada que **reduz a complexidade** dos diagramas tradicionais. Em vez de representar cada detalhe, oferece uma **visão em camadas**.
- Diferentes públicos entendem a arquitetura **sem sobrecarga** de informação.
- Destaca-se pela **simplicidade e modularidade**.
- Evita problemas de comunicação, como ambiguidades sobre responsabilidades e confusões sobre dependências.
- **Exemplo de uso**: o time de vendas mostra o diagrama de **Contexto** a um cliente novo; os devs usam **Contêiner** e **Componente** para implementar.

## C4 × HLD × LLD
| | HLD | LLD | C4 Model |
|---|---|---|---|
| Foco | Visão macro: componentes maiores e fluxos de dados | Detalhes técnicos: classes, métodos e suas interações | **Transição gradual** entre o geral (como no HLD) e o específico (como no LLD) |
| Ponto forte | Início do projeto: o que o sistema faz e quem usa | Fase de desenvolvimento | Cada público vê o nível relevante |
| Limitação | Pode faltar detalhe para quem implementa | Pode faltar uma visão integrada | Não citada |

A comparação visual está na Figura 2 do PDF.

## Os 4 níveis
| Nível | Responde ou mostra | Comparável a | Resolve | Exemplo (sistema bancário) |
|---|---|---|---|---|
| **1. Contexto** | "Qual é o propósito do sistema?" e "Quem usa ou interage com ele?": usuários e sistemas externos | **HLD** (o C4 tende a detalhar as interações com mais clareza) | Falta de alinhamento entre equipes | Um perfil de usuário e a comunicação com outros serviços, como um **mainframe** |
| **2. Contêiner** | Os grandes blocos (bancos de dados, APIs, servidores, front-end, back-end) e como interagem | **Intermediário** entre HLD e LLD | Dependências e responsabilidades (ex.: um módulo dependendo demais de outro compromete a escalabilidade); visualizar o fluxo de dados | Servidor web, banco de dados de produtos e serviço de API, independentes mas interconectados |
| **3. Componente** | Os módulos internos de cada contêiner e como interagem | Não citado | **Coesão e modularidade**: entender a função de cada módulo, onde implementar ou alterar algo | Num contêiner de acesso: autenticação, envio de e-mail, confirmação de transação |
| **4. Código** | A implementação interna: estrutura de classes, organização do código | Não citado | Auditorias de código, manutenção, continuidade | Consulta de saldo: cada etapa do cálculo (conversão de moedas, aplicação de taxas) |

> [!important] O nível de Código é **opcional**
> Use-o só quando os detalhes de implementação precisarem ser registrados.

## System Landscape
Os 4 níveis mostram uma **visão estática de um sistema isolado**, mas na prática os sistemas nunca funcionam sozinhos. O **system landscape diagram** é um "mapa" dos sistemas de uma empresa, organização ou departamento. É basicamente um **diagrama de contexto sem foco num sistema específico** (Figura 6 do PDF).

## Dicas de uso
- **Contexto**: alinhar o entendimento entre equipes técnicas e de negócio.
- **Contêiner**: identificar e definir as responsabilidades dos módulos principais.
- **Componente**: detalhar módulos complexos e organizar a arquitetura em partes gerenciáveis.
- **Código**: só em casos específicos, quando o detalhamento profundo for necessário.

## Referências
Brown, *The C4 Model – Misconceptions, Misuses & Mistakes* (YouTube, 2023) · Brown, *The C4 model for visualizing software architecture* (2022) · Santana e Rossalli, *C4-Model: por que documentar a arquitetura dos seus projetos?* (Zup, 2022)
