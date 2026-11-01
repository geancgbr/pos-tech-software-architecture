---
tags: [pos-tech/fase-2, devops, revisao]
disciplina: DevOps (IaC and CI/CD)
---

# Revisão - DevOps (IaC and CI/CD)

[[DevOps (IaC and CI-CD)]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - CI/CD
> [!question]- O que o DevOps promove, segundo a aula 1?
> Por uma cultura de colaboração, desenvolvimento e manutenção com foco em qualidade. A integração contínua é a base para toda a automação funcionar. → [[DevOps]]

> [!question]- O que é integração contínua?
> Uma técnica em que os devs colocam o código num único repositório, para eliminar problemas e retrabalho e facilitar a localização de erros. → [[Integração Contínua (CI)]]

> [!question]- De qual metodologia vem a integração contínua, e quem criou essa metodologia e quando?
> Do Extreme Programming (XP), criado em 1996 por Kent Beck. → [[Extreme Programming (XP)]]

> [!question]- Com que frequência cada dev deve integrar o código, segundo a prática de XP?
> Ao menos uma vez por dia.

> [!question]- Cite as Boas Práticas de XP.
> Cliente sempre disponível, uso de metáforas, planejamento do jogo, pequenas versões, simplicidade de projeto, melhoria constante, testes de aceitação, testes em primeiro lugar e integração contínua.

> [!question]- Quais são as etapas do fluxo de trabalho manual?
> Integração do código-fonte, compilação ou build, verificação ou testes, e implantação ou deploy.

> [!question]- Por que algumas empresas ainda usam o modelo manual?
> Porque não estão amadurecidas para implantar testes efetivos e automatizados.

> [!question]- Como Paul Duvall define a integração contínua?
> Como a peça central do desenvolvimento, que garante a integridade do software executando um build a cada mudança.

> [!question]- Quais são os valores da integração contínua?
> Redução de riscos, redução dos processos manuais repetitivos, software implantável a qualquer momento, maior visibilidade do projeto e maior confiança no software produzido.

> [!question]- Entrega contínua × deploy contínuo?
> Entrega contínua: cada mudança pode ir para produção, mas a equipe pode optar por não implantar (geralmente por motivos comerciais); o pacote fica pronto, testado e guardado num repositório de artefatos. Deploy contínuo: cada pacote vai para produção automaticamente, sem intervenção humana, quando cumpre os requisitos da esteira. → [[Entrega Contínua e Deploy Contínuo]]

> [!question]- É possível ter deploy contínuo sem entrega contínua?
> Não. Para haver deploy contínuo, é preciso ter entrega contínua.

> [!question]- Por que trabalhar em pequenos lotes?
> Reduz o tempo de feedback, facilita a triagem e a correção, aumenta a eficiência e a motivação, evita a falácia do custo irrecuperável e reduz o risco da mudança. A entrega contínua torna isso economicamente viável.

## Aula 2 - GitHub e branches
> [!question]- O que é um sistema de controle de versão?
> Um sistema que registra as alterações de arquivos ao longo do tempo para recuperar versões específicas depois (Chacon e Straub). → [[Controle de Versão]]

> [!question]- Versionamento centralizado × distribuído?
> Centralizado: um único servidor; é um ponto único de falha. Ferramentas: CVS, Apache Subversion. Distribuído: cada dev tem o repositório completo, com histórico; o time continua se o servidor cair, mas exige mais disciplina e pode gerar conflitos. Ferramentas: GitHub, Bitbucket, GitLab.

> [!question]- Qual modelo é o mais indicado para integração contínua, e por quê?
> O distribuído, porque vários times trabalham em paralelo (ex.: qualidade com os testes automatizados, infraestrutura com as automações de provisionamento).

> [!question]- Quais são os critérios para escolher um workflow?
> Produtividade, coerência (tamanho da equipe), praticidade (desfazer erros) e simplicidade (carga cognitiva). → [[Workflows de Branches (GitHub Flow, OneFlow, GitFlow)]]

> [!question]- Qual é a regra principal do GitHub Flow?
> Tudo na master/main pode ser entregue. Se houver problemas em commits, eles são revertidos ou novos commits são adicionados.

> [!question]- Quando o GitHub Flow não é recomendado?
> Para releases de homologação e quando são necessárias várias versões em produção. Também há o risco de o código em produção ficar instável.

> [!question]- Qual é a condição principal do OneFlow?
> Toda nova versão em produção é baseada na release anterior. Existe uma única branch de produção, e as outras são temporárias.

> [!question]- Quem criou o GitFlow, e quais são as duas branches principais?
> Vincent Driessen (2010). As branches são a master (produção) e a develop (em andamento).

> [!question]- Quais são as branches de suporte do GitFlow?
> feature (novas funcionalidades), release (testes e empacotamento para produção) e hotfix (correção imediata de erro em produção).

> [!question]- Merge × rebase?
> O rebase deixa o histórico mais limpo. O merge cria uma linha de histórico no ponto da integração, o que é mais complexo de ler, mas mais seguro, porque não sobrescreve código. O ideal é analisar caso a caso.

> [!question]- Qual workflow não tem release branches?
> O GitHub Flow.

## Aula 3 - Testes automatizados com CI
> [!question]- Como o DevOps leva o modelo ágil um passo adiante?
> Aproximando o lançamento e a implantação do desenvolvimento e do teste: a equipe ágil, sozinha, desenvolve, testa e lança.

> [!question]- Além de testes funcionais, pelo que os testadores respondem no DevOps?
> Testes de operações, de desempenho, testes básicos de segurança, e monitoramento e análise de dados e registros de produção.

> [!question]- Qual é o único processo totalmente manual da integração contínua?
> O TDD: o dev cria um teste que falha em 100% das tentativas e vai escrevendo o código até ficar pronto. → [[TDD (Test-Driven Development)]]

> [!question]- Teste automático × teste contínuo?
> Automático: executado por estímulo humano (comando, IDE). Contínuo: executado automaticamente a cada alteração no repositório, num workflow que só segue se os testes passarem. → [[Testes Contínuos]]

> [!question]- Que percentual dos testes os testes técnicos representam, e por quê?
> 90%, principalmente porque um erro encontrado nessa fase custa menos (custo, esforço e tempo) do que nas fases seguintes.

> [!question]- Qual é a base dos testes de software, segundo a aula 3?
> Os testes "técnicos": integração, componentes e unitários.

> [!question]- O que o pipeline deve executar?
> Os mesmos "comandos" que o dev executa, principalmente nos testes unitários (ex.: `mvn test`/`mvn verify`, `dotnet test`, `npm test`, `pytest`).

> [!question]- Qual é a boa estratégia de testes automatizados no pipeline?
> Testar tudo o que for possível, dos testes unitários (ligados à CI) aos funcionais em homologação e produção.

## Aula 4 - Qualidade do código-fonte
> [!question]- O que é qualidade do código-fonte?
> Uma medida de quão bem escrito, organizado, eficiente e confiável é o código, e da sua capacidade de atender aos requisitos funcionais e não funcionais. → [[Qualidade do Código-Fonte]]

> [!question]- Quais são as características de qualidade do código?
> Legibilidade, eficiência, confiabilidade, escalabilidade, manutenibilidade e segurança.

> [!question]- Cite práticas colaborativas para a qualidade do código.
> Code reviews, pair programming e sessões de depuração conjunta.

> [!question]- Cite exemplos de baixa qualidade do código.
> Duplicação, falta de coesão, complexidade excessiva, falta de documentação, falta de validação de entrada, ausência de testes automatizados, falta de otimização, variáveis confusas, falta de modularização, condicionais em excesso e falta de tratamento de exceções.

> [!question]- Falso positivo × falso negativo numa ferramenta de análise?
> Falso positivo: aponta um problema que não existe (perda de tempo). Falso negativo: não aponta um problema real.

> [!question]- Quais são os desafios de analisar código legado?
> Dificuldade de integração, limitações na detecção, maior número de problemas, e restrições de tempo e orçamento. A abordagem deve ser estratégica, e a modernização é gradual.

> [!question]- Qual ferramenta é uma extensão do Visual Studio para C# e .NET?
> O ReSharper.

> [!question]- O que se cria no SonarQube no Hands On?
> Quality Profiles e Quality Gates, sincronizados com a esteira do GitHub. → [[SonarQube]]

## Dúvidas em aberto
- [ ] **IaC**: nenhuma das 4 aulas trata de Infraestrutura como Código, apesar do nome da disciplina.
- [ ] **Tabela de comparação de workflows** (aula 2, pág. 16): a linha de rebasing sai embaralhada na extração do texto. Conferir no PDF.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
