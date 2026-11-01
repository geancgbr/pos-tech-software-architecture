---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 6
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 6.pdf"
---

# DOC 06 - DAS (Design Approval Sheet)

← [[DOC 05 - Architecture Decision Records (ADRs)]] · [[Documentação de Arquitetura de Soluções]]

> [!summary] Em uma frase
> O [[DAS (Design Approval Sheet)|DAS]] é o **documento mestre** que consolida e aprova as escolhas feitas no projeto. As aulas anteriores (HLD/LLD, C4, requisitos e ADRs) são a base para entendê-lo. Funciona como um "guia ou contrato" e como **mecanismo de controle** na governança de arquitetura.

## Hands On (vídeo)
Um template de DAS **preenchido** com os elementos e decisões discutidos na aula.

## O que é e por que importa
- É apresentado depois de [[HLD e LLD (High-Level Design e Low-Level Design)|HLD, LLD]], [[C4 Model]], [[Requisitos Funcionais e Não Funcionais|requisitos funcionais e não funcionais]] e [[ADR (Architecture Decision Record)|ADRs]]. Esses conceitos são a base para entender cada parte do DAS, que consolida e aprova as escolhas feitas no projeto.
- É um **documento mestre** com as decisões importantes, como um guia ou contrato: cada escolha técnica documentada, com o "porquê". **Formaliza** as decisões e dá uma referência sólida ao time e aos stakeholders.
- **Sem ele**: as equipes ficam mais propensas a perder o controle das decisões, o que pode gerar retrabalho e problemas mais graves.
- **Útil principalmente com várias equipes**: alinha expectativas, evita conflitos e funciona como **ponte** entre times.
- **Evolui com o projeto**: registra e justifica as mudanças e mantém a flexibilidade.

## Os 11 elementos da estrutura
| # | Elemento | Conteúdo |
|---|---|---|
| 1 | **Identificação do projeto** | Título, versão, data de criação, identificador único (controle e histórico) |
| 2 | **Descrição do contexto** | Circunstâncias, restrições e justificativas das decisões: o "porquê" |
| 3 | **Requisitos e restrições** | Funcionais (recursos, ações) e não funcionais (desempenho, segurança, escalabilidade) |
| 4 | **Diagrama de arquitetura** | Contexto, contêineres e componentes (**C4**); diagramas de **sequência** e de **implantação** |
| 5 | **Decisões de arquitetura (ADR)** | Decisão, contexto, alternativas, justificativas, consequências |
| 6 | **Plano de testes e monitoramento** | Tipos de teste (unitários, integração, carga) e ferramentas e métricas de monitoramento em produção |
| 7 | **Modelo de dados** | Entidades e relacionamentos; diagrama entidade-relacionamento |
| 8 | **Documentação de API** | Endpoints, métodos HTTP, parâmetros, cabeçalhos, exemplos de resposta |
| 9 | **Manual de instalação e configuração** | Passo a passo por ambiente (desenvolvimento, testes, produção) |
| 10 | **Plano de continuidade e backup** | Para sistemas críticos: operação em caso de falhas e rotinas de backup |
| 11 | **Planos de segurança e compliance** | Se houver dados sensíveis ou regulamentação: autenticação, controle de acesso, criptografia, conformidade (**LGPD, GDPR, PCI-DSS**) |

A estrutura pode variar de acordo com o projeto. Antes de preencher, a apostila recomenda **revisar as aulas anteriores**.

## O template da aula (Quadro 1)
O template também está em "Materiais complementares", no menu da fase.

```text
Design Approval Sheet (DAS)
Projeto: [Nome do Projeto]   Data: [Data de Criação]   Versão: [Versão]   Identificador: [Identificador Único do DAS]

Contexto do Projeto ............ panorama geral, objetivos, valor para usuários e empresa
Requisitos do sistema .......... funcionais (funcionalidades) e não funcionais (desempenho, segurança, disponibilidade...)
Arquitetura e tecnologias ...... front-end, back-end, banco, autenticação, infraestrutura, com justificativa
Estrutura da arquitetura (C4) .. Contexto (C1), Container (C2), Componentes (C3)
Diagramas de arquitetura ....... contexto, containers, componentes, sequência de processos
Restrições e decisões técnicas . ex.: escolha de banco de dados, provedores de infraestrutura
Documentação de RF e RNF ....... funcionalidades e métricas de cada requisito não funcional
Diagrama de implantação ........ configuração de infraestrutura, instalação e configuração
ADR ............................ contexto, decisão, alternativas, impacto de cada decisão
Plano de testes e monitoramento  tipos de teste, ferramentas de monitoramento e alertas
Modelo de dados ................ DER com tabelas e relacionamentos
Documentação de API ............ endpoints, métodos HTTP, parâmetros, exemplos de resposta
```

> [!note] No template, a seção de C4 vai só até **C3** (Componentes). O nível de Código não aparece.

## Como criar
1. **Coletar todos os requisitos** com os stakeholders, principalmente os que influenciam o design.
2. **Consultar especialistas e discutir alternativas**, analisando cada decisão.
3. Justificar cada escolha, como um histórico de "porquês" e "comos".

## Governança
- O DAS é um **mecanismo de controle**: garante que as decisões estejam em conformidade com as **políticas e normas da organização** (qualidade e segurança).
- Em projetos grandes, com várias equipes e camadas de autorização, as decisões são documentadas e acompanhadas. Governança significa **criar, monitorar e atualizar** o documento.
- Deve ser um **registro vivo**, para acompanhar riscos de forma proativa e evitar problemas de integração entre módulos.

## Vantagens, desafios e quando não usar
- **Vantagens**: **transparência e rastreabilidade** · **consistência** · comunicação, porque centraliza informações, elimina ambiguidades e reduz reuniões longas.
- **Desafios**: é **trabalhoso** e há resistência à formalização. Veja-o como investimento contra retrabalho.
- **Quando não é necessário**: em **projetos pequenos**, a formalização excessiva pesa. Adapte à realidade de cada projeto.

## Ferramentas
**Confluence, Word e Google Docs**: compartilhamento em tempo real e modelos prontos e customizáveis. Templates padronizados dão consistência. A integração com as ADRs numa ferramenta centralizada fortalece a governança.

## Referências
Brown, *C4 Model* · Microsoft, *ADRs* · Richards e Ford, *Fundamentals of Software Architecture* (2020) · Rozanski e Woods, *Software Systems Architecture* (2012)
