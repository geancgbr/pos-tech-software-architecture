---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 1
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 1.pdf"
---

# DOC 01 - Introdução à documentação de arquitetura

[[Documentação de Arquitetura de Soluções]] · Próxima → [[DOC 02 - High-Level Design (HLD) e Low-Level Design (LLD)]]

> [!summary] Em uma frase
> A [[Documentação de Arquitetura|documentação de arquitetura]] registra o desenho e as decisões técnicas de um sistema (estrutura, componentes, interações e os **motivos** das escolhas). Sem ela, cada mudança vira engenharia reversa, e uma parte significativa do conhecimento pode se perder com quem sai da equipe.

## Hands On (vídeo)
Uma visão introdutória de cada tipo de documentação: quando usar, por que é importante e as boas práticas para mantê-la útil e atualizada.

## Por que documentar
- **Cenário da aula**: um time herda um sistema antigo, com vários módulos e integrações, sem documentação, e com muitos dos devs que programaram o código já fora da empresa. Cada mudança fica arriscada e demorada, porque é preciso "descobrir" como o sistema foi construído e quais dependências podem ser afetadas.
- **O que a documentação faz**:
  - serve de **guia** para novos membros e para decisões futuras: o que foi feito e **por quê**;
  - **alinha as áreas** da empresa numa visão comum e evita conhecimento fragmentado;
  - **preserva o conhecimento** quando colaboradores saem, o que é crítico em empresas com alta rotatividade;
  - mostra aos devs como o sistema deve funcionar, o que **diminui o retrabalho**;
  - melhora a comunicação entre stakeholders técnicos e não técnicos.
- **Sem documentação**:
  - a compreensão do histórico fica difícil, e a **engenharia reversa** reduz a produtividade e aumenta os erros;
  - há altos custos para recuperar o conhecimento e problemas operacionais;
  - cresce a resistência a novas práticas e tecnologias;
  - corrigir um bug sem registro das dependências entre módulos torna o impacto das mudanças **imprevisível**.
- **Outro cenário da aula**: um fornecedor entrega só um Word genérico, sem jornadas e sem visão da integração, e você fica dependente da única pessoa que desenvolveu o sistema.

## Os tipos de documentação
| Documento | O que é | Quando e como usar |
|---|---|---|
| **[[ADR (Architecture Decision Record)\|ADR]]** | Registra as escolhas técnicas: o que foi decidido, por quê, as alternativas e as implicações. Garante rastreabilidade | Sempre que houver uma decisão arquitetural importante (framework, mudança de arquitetura, funcionalidade que impacte outros componentes). Formato padrão: **decisão, contexto, status e consequências**. A Figura 2 mostra um template de ADR de Michael Nygard |
| **[[DAS (Design Approval Sheet)\|DAS]]** | Documento **formal** que registra as decisões de design e arquitetura para **validação e aprovação** dos stakeholders. É um **marco**: todos concordam antes da implementação | Nas fases de aprovação e revisão do design. Pode ser revisitado depois. Simples e direto, com justificativas. A **assinatura ou confirmação digital** de cada parte pode ser uma prática útil para formalizar o processo |
| **[[HLD e LLD (High-Level Design e Low-Level Design)\|HLD]]** | **Estrutura global** do sistema e como os componentes principais se interconectam (módulos, sistemas externos, padrões de comunicação), **sem detalhar a implementação** | Revisitado durante o desenvolvimento. Inclua diagramas de interação e descrições dos componentes. É a **base para o LLD** |
| **[[HLD e LLD (High-Level Design e Low-Level Design)\|LLD]]** | Descrição **detalhada** de cada componente: classes, métodos, algoritmos, fluxos de dados, interações | Usado **após o HLD**. Referência na implementação e para verificar a conformidade do código. Em ciclos ágeis, pode ser atualizado à medida que novos detalhes são definidos. Inclua diagramas de classes e fluxos de processo |
| **[[C4 Model]]** | Representa o sistema em **níveis de abstração**: Context, Container, Component, Code | Projetos complexos, com várias equipes que precisam entender a arquitetura em níveis diferentes |
| **Requisitos funcionais** | O que o sistema deve realizar (registro de usuário, processamento de transações...) | No levantamento de requisitos. Guia o desenvolvimento e os testes e serve de referência para os casos de teste |
| **Requisitos não funcionais** | Características de qualidade: desempenho, segurança, escalabilidade, disponibilidade, manutenibilidade. É **como** o sistema deve se comportar | Alinham expectativas e definem benchmarks para testes de desempenho e segurança. Revisite-os nos testes e na operação |
| **[[Diagrama de Sequência]]** | Interação entre componentes ou objetos **ao longo do tempo** numa funcionalidade | No design detalhado de funcionalidades críticas com vários componentes. Ajuda a achar gargalos e pontos de falha. Foque nas interações importantes e use identificadores claros |

**Outros documentos citados**
- **Diagrama de classe**: classes e relações, usado no design detalhado e na implementação.
- **Diagrama de componentes**: componentes principais e dependências, usado no design arquitetural e na integração (acoplamentos).
- **Manual de instalação e configuração**: consistência entre ambientes; apoia DevOps e administradores.
- **Plano de testes**: unitários, integração, carga, do desenvolvimento à produção.
- **Modelo de dados**: tabelas e relacionamentos, importante para a camada de persistência.
- **Documentação de API**: endpoints e métodos. Precisa de atualização constante, principalmente em **microsserviços**.

## Boas práticas
- **Organização e acesso**: Confluence, Google Docs ou ferramentas como LeanX, Mega ou Ardoq, para centralizar o conhecimento para equipes técnicas e não técnicas.
- **Colaboração**: o conhecimento distribuído no time, não concentrado em poucas pessoas. Processos claros de atualização (como reuniões) mantêm a documentação **viva**.
- **Revisão periódica**, com responsáveis em cada fase.
- **Automação**: Swagger para APIs e CI/CD para diagramas de infraestrutura.
- **Cultura de documentação** integrada aos ciclos de desenvolvimento (ex.: metodologias ágeis), para vencer a falta de tempo e a resistência dos times.

## Mercado, cases e tendências
Leitura recomendada: *Software Architecture in Practice* (Bass, Clements e Kazman, 2012).

## Referências
Bass, Clements e Kazman (2012) · Brown, *C4 Model* · Nygard, *Documenting Architecture Decisions* (2011) · Visual Paradigm
