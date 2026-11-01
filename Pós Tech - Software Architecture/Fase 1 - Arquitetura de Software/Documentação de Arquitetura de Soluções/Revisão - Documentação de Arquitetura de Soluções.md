---
tags: [pos-tech/fase-1, documentacao, revisao]
disciplina: Documentação de Arquitetura de Soluções
---

# Revisão - Documentação de Arquitetura de Soluções

[[Documentação de Arquitetura de Soluções]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- O que é a documentação de arquitetura?
> A base que registra o desenho e as decisões técnicas de um sistema: estrutura, componentes, interações e os motivos das escolhas. → [[Documentação de Arquitetura]]

> [!question]- Cite problemas da falta de documentação.
> Dificuldade de entender o histórico (engenharia reversa, menos produtividade, mais erros), perda de conhecimento quando alguém sai, resistência a novas práticas e impacto imprevisível das mudanças (ex.: corrigir um bug sem conhecer as dependências).

> [!question]- O que um ADR documenta, e qual é o formato padrão citado na aula 1?
> As escolhas técnicas: o que foi decidido, os motivos, as alternativas e as implicações. Formato padrão: decisão, contexto, status e consequências. → [[ADR (Architecture Decision Record)]]

> [!question]- O que é o DAS, e que prática a aula 1 sugere para formalizar a aprovação?
> Um documento formal que registra as decisões de design e arquitetura para validação e aprovação dos stakeholders, antes da implementação. A assinatura ou confirmação digital de cada parte pode ser uma prática útil para formalizar o processo. → [[DAS (Design Approval Sheet)]]

> [!question]- Requisito funcional × requisito não funcional (aula 1)?
> Funcional: o que o sistema deve realizar. Não funcional: características de qualidade (desempenho, segurança, escalabilidade, disponibilidade, manutenibilidade), ou seja, como o sistema deve se comportar.

> [!question]- Para que serve o diagrama de sequência?
> Para representar a interação entre componentes ou objetos ao longo do tempo numa funcionalidade, ajudando a identificar gargalos e pontos de falha. → [[Diagrama de Sequência]]

> [!question]- Cite boas práticas para manter a documentação útil.
> Ferramentas centralizadas (Confluence, Google Docs, LeanX, Mega, Ardoq), colaboração, processos de atualização, revisão periódica, automação (Swagger, CI/CD) e cultura de documentação.

## Aula 2 - HLD e LLD
> [!question]- HLD × LLD?
> HLD: visão macro (componentes principais e relações) para alinhar com os stakeholders, sem detalhar a implementação. LLD: detalhes técnicos de cada componente (classes, métodos, algoritmos, fluxos), especificando serviços, tecnologias, linguagens e fornecedores. → [[HLD e LLD (High-Level Design e Low-Level Design)]]

> [!question]- Qual vem primeiro?
> O HLD. O LLD é desenvolvido em seguida, para detalhar cada componente.

> [!question]- Quais elementos compõem um HLD eficaz?
> Visão geral do sistema (objetivo e funcionalidades), diagrama de arquitetura (componentes-chave e interações) e lista de requisitos de alto nível.

> [!question]- O que acontece sem HLD?
> Dificuldade de alinhamento, interpretações divergentes, retrabalho, desperdício, incompatibilidades, atrasos e custos maiores.

> [!question]- Quais elementos fazem parte do LLD?
> Fluxos de dados, algoritmos, especificações de interfaces e diagramas técnicos, como fluxogramas e diagramas de sequência.

> [!question]- Fluxograma × diagrama de sequência no LLD?
> O fluxograma ilustra o fluxo de um processo específico. O diagrama de sequência detalha a interação entre os componentes.

## Aula 3 - C4 Model
> [!question]- Quem criou o C4 Model, e quais são os 4 níveis?
> Simon Brown. Contexto, Contêiner, Componente e Código. → [[C4 Model]]

> [!question]- Qual nível do C4 é opcional?
> O de Código.

> [!question]- Quais perguntas o diagrama de Contexto responde?
> "Qual é o propósito do sistema?" e "Quem usa ou interage com o sistema?".

> [!question]- Qual nível do C4 é comparável ao HLD, e qual é intermediário entre HLD e LLD?
> O Contexto é comparável ao HLD. O Contêiner é intermediário.

> [!question]- Que problema o diagrama de Componente resolve?
> Problemas de coesão e modularidade: entender a função de cada módulo e onde implementar ou alterar uma funcionalidade.

> [!question]- O que é o System Landscape diagram?
> Um "mapa" dos sistemas de uma empresa, organização ou departamento. É basicamente um diagrama de contexto sem foco num sistema específico.

> [!question]- Como o C4 se relaciona com HLD e LLD?
> Faz uma transição gradual entre a visão geral (como no HLD) e os detalhes (como no LLD), para que cada público veja o nível relevante.

## Aula 4 - Requisitos funcionais e não funcionais
> [!question]- Dê um exemplo de requisito funcional e um de não funcional da aula.
> Funcional: "permitir que o usuário transfira fundos entre contas". Não funcional: "responder a solicitações em até 2 segundos" ou "suportar até 10.000 usuários simultâneos". → [[Requisitos Funcionais e Não Funcionais]]

> [!question]- Qual é o primeiro passo do levantamento de requisitos?
> Envolver os stakeholders em reuniões, para um entendimento profundo e informações completas.

> [!question]- Modelo tradicional × atual de construção de requisitos?
> Tradicional: todos os requisitos definidos no início ("coletar"), pelo analista de sistemas; burocrático e pouco adaptável. Atual: colaborativo, com feedback contínuo, reconhecendo que é impossível prever tudo no início.

> [!question]- Qual é o papel do PM, do PO, do time técnico e da arquitetura?
> PM: define a visão do produto. PO: traduz a visão em histórias de usuário. Time técnico: testa, refina e dá feedback. Arquitetura: garante a coerência técnica e o alinhamento de longo prazo.

> [!question]- O que faz o arquiteto de soluções?
> É o elo entre o negócio e a implementação: entende as necessidades, define a estrutura e os componentes, toma decisões estratégicas, seleciona tecnologias, estabelece padrões, mitiga riscos e coordena as interações entre os papéis. → [[Arquiteto de Soluções]]

> [!question]- Cite boas práticas de documentação de requisitos.
> Lista clara e detalhada, linguagem objetiva, validação com os stakeholders, organização por prioridade, documentação atualizada e templates padronizados.

## Aula 5 - ADRs
> [!question]- O que acontece com uma ADR depois de aceita?
> Ela se torna imutável. Para mudar, cria-se uma nova ADR, e a anterior recebe o estado "Superada". → [[ADR (Architecture Decision Record)]]

> [!question]- O que é o log de decisões?
> O conjunto das ADRs, que forma o histórico das escolhas do time e dá a visão contextual do projeto.

> [!question]- Qual é o mínimo que cada ADR deve ter?
> Contexto, decisão e consequências.

> [!question]- Quais são as 4 seções principais da ADR na aula 5?
> Contexto, Decisão, Consequências e Alternativas.

> [!question]- Quais status aparecem no quadro "Como implementar uma ADR"?
> Proposta, Aceita, Depreciada, Substituída e Rejeitada.

> [!question]- Qual é o papel do "dono(a)" da ADR?
> Manter a ADR, comunicar o conteúdo, conduzir a revisão e aprovar as alterações.

> [!question]- Cite decisões que justificam uma ADR.
> Estrutura do sistema (microsserviços), requisitos não funcionais (segurança, alta disponibilidade), dependências entre componentes, interfaces (APIs, contratos) e técnicas de construção (bibliotecas, ferramentas, processos). Em geral, decisões difíceis de reverter.

> [!question]- Quando não usar ADR?
> Em decisões triviais ou temporárias (use changelog ou versionamento) e em prototipagem com iterações rápidas, onde o excesso gera "dívida de documentação".

> [!question]- Quais são as consequências de não usar ADRs?
> O "porquê" se perde, surgem decisões conflitantes (ex.: dois métodos de autenticação) e decisões são revertidas sem análise, gerando retrabalho e débito técnico.

## Aula 6 - DAS
> [!question]- O que é o DAS, segundo a aula 6?
> Um documento mestre que consolida e aprova as decisões do projeto: um guia ou contrato, com o porquê de cada escolha técnica. → [[DAS (Design Approval Sheet)]]

> [!question]- Cite os elementos da estrutura do DAS.
> Identificação do projeto, contexto, requisitos e restrições, diagramas de arquitetura, ADRs, plano de testes e monitoramento, modelo de dados, documentação de API, manual de instalação e configuração, plano de continuidade e backup, e segurança e compliance.

> [!question]- O que vai na identificação do projeto?
> Título, versão, data de criação e identificador único.

> [!question]- Quais regulamentações a seção de segurança e compliance cita?
> LGPD, GDPR e PCI-DSS.

> [!question]- Qual é o papel do DAS na governança?
> É um mecanismo de controle que garante a conformidade das decisões com as políticas e normas da organização. Precisa ser criado, monitorado e atualizado.

> [!question]- Quais são as vantagens e os desafios do DAS?
> Vantagens: transparência, rastreabilidade, consistência e comunicação. Desafios: é trabalhoso e há resistência à formalização.

> [!question]- Quando o DAS não é necessário?
> Em projetos pequenos, onde a formalização excessiva pesa.

## Dúvidas em aberto
- [ ] **ADR**: a aula 1 dá o formato "decisão, contexto, status e consequências", e a aula 5 dá as seções "Contexto, Decisão, Consequências, Alternativas". Os nomes dos estados também variam: o texto do processo usa "Superada", e o quadro usa "Substituída" (substituída por outra). O quadro tem ainda "Depreciada" (não faz mais sentido), que é um estado diferente. Ver qual versão o professor usa.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
