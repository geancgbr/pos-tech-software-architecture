---
tags: [pos-tech/fase-4, microsservicos, testes, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 4
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 4.pdf"
---

# MS2 04 - Testando microsserviços, parte 2

← [[MS2 03 - Testando microsserviços]] · [[Estrutura de Microsserviços Parte II]] · Próxima → [[MS2 05 - Realizando o deploy de microsserviços]]

> [!summary] Em uma frase
> Os testes de **integração, componente, ponta a ponta e contrato**, no Hands On e no resumo. O texto do PDF trata de **CI/CD e testes** (chegando ao **Continuous Deployment**), da **análise de qualidade de código** ([[SonarQube]], linters, métricas), dos **testes de segurança** (**SAST** e **DAST**) e do **[[BDD (Behavior-Driven Development)|BDD]]** com **Gherkin**.

## Hands On
Implementar os **testes de integração** do **Catálogo** (incluindo um teste da **API**), ver um **teste de contrato** pelo lado do **consumidor** e desenvolver os **testes de componente**. Repositório da aula 4.

**Segundo o resumo**:
- **Teste de integração de persistência**: valida a integração entre o serviço e o **banco**.
- **Testes de contrato de API**: **consumer-side** e **consumer-driven**, que testam o uso da API pela perspectiva **do serviço e dos consumidores**.
- **Teste de componente**: testa o **serviço como um todo**, abstraindo as dependências.
- **Teste de ponta a ponta**: **pode ser custoso**, dada sua fragilidade e complexidade; é estratégico focar nas **jornadas de usuário mais importantes**.

## CI/CD e testes
- **CI**: cada **commit** dispara testes automatizados, que **podem incluir** unitários, integração, componente e ponta a ponta, com **feedback instantâneo**. Ver [[Integração Contínua (CI)]].
- **CD (Continuous Delivery)**: automatiza a implantação de um commit aprovado; antes, podem rodar **testes de contrato**.
- **Publicação Contínua (Continuous Deployment)**: com testes cobrindo os cenários, toda mudança que passa nos testes vai **para produção sem aprovação de alguém**. Ver [[Entrega Contínua e Deploy Contínuo]].
- **Vantagens**: **isolamento de falhas** · **rapidez** (cada equipe com seu pipeline) · **garantia de qualidade**.

## Análise de qualidade de código
- Avalia **legibilidade, manutenibilidade e eficiência**; em microsserviços, ajuda a **mitigar potenciais** problemas que afetam toda a cadeia de integração.
- **SonarQube**: inspeção **contínua**, relatórios, **pode ser integrado** ao **CI/CD** (verificação a cada commit) e sugestões de correção.
- **Linters**: análise estática em busca de erros, bugs e padrões inconsistentes; **podem ser configurados** para seguir um **guia de estilo** e muitos **corrigem automaticamente**. Ver [[Análise Estática de Código]].

| Métrica | O que mede |
|---|---|
| **Complexidade ciclomática** | A complexidade do código; o que pode ser refatorado |
| **Débito técnico** | O custo de **adiar** refatorações e correções |
| **Cobertura de testes** | A **porcentagem** do código efetivamente testada |

- **Vantagens**: **padronização** entre equipes (ex.: meta de % de cobertura) · **refatoração orientada** · **integração com CI/CD**.

## Testes de segurança
Especialmente importantes em microsserviços, pela natureza **distribuída** e pelas muitas **APIs** expostas: buscam vulnerabilidades contra **integridade, confidencialidade ou disponibilidade**.
- **Tipos comuns**: **injeção** (SQL Injection, XSS) · **autenticação e autorização** · **negação de serviço (DoS)**. Ver [[SQL Injection e Command Injection]] e [[XSS (Cross-Site Scripting)]].
- **Práticas**: integrar ao **CI/CD** (ferramentas **SAST e DAST**, como o **Fortify**) · **auditorias** regulares · **treinamento** da equipe.

| | SAST (Static Application Security Testing) | DAST (Dynamic Application Security Testing) |
|---|---|---|
| Como | Analisa o **código-fonte**, **sem executar** o aplicativo | Analisa o aplicativo **em execução**, **simulando ataques** |
| Encontra | Falhas de segurança, **vazamentos de memória**, não conformidade com padrões | **XSS**, **injeção de SQL** e vulnerabilidades da operação normal; útil em **apps web e APIs** |

## BDD
- **Behavior-Driven Development**: estende o **TDD**, com foco no **comportamento** e na **colaboração**. Responde "**O que o sistema deve realizar?**" em vez de "Como vamos implementá-lo?".
- Usa **linguagem natural** para comportamentos e requisitos, aproximando pessoas não técnicas e devs; de uma descrição de alto nível para **cenários** em sentenças simples.
- **Gherkin**: **Given** [contexto inicial] · **When** [uma ação ocorre] · **Then** [resultado esperado].
- **Ferramentas**: **Cucumber, JBehave, SpecFlow**, que executam as especificações como testes automatizados.
- Os cenários **podem ser** incorporados a pipelines de **CI/CD**. **Desafio**: **manutenção**, porque os cenários podem ficar obsoletos.

> [!note] O "O que vem por aí", o Hands On e o resumo tratam de testes de integração, componente, ponta a ponta e contrato; o Saiba Mais do PDF trata de outros temas (CI/CD, qualidade de código, segurança e BDD).

## Referências
Fowler: IntegrationTest · Pact: Introduction · Richardson, *Microservices Patterns* · Richardson: Service Integration Contract Test
