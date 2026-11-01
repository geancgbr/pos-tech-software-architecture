---
tags: [pos-tech/fase-2, github-actions, revisao]
disciplina: GitHub Actions
---

# Revisão - GitHub Actions

[[GitHub Actions]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- O que é o GitHub Actions, e quando foi lançado?
> Uma plataforma de automação do GitHub, incorporada ao gerenciamento de repositórios, para criar, personalizar e executar pipelines de CI/CD. Foi lançada em 2018. → [[GHA 01 - Introdução]]

> [!question]- Quais são os dois componentes da integração contínua, segundo a aula?
> Um componente de automação (uma ferramenta de CI ou um serviço de compilação) e um componente cultural (a mentalidade de integrar com frequência).

> [!question]- Quais são os objetivos da integração contínua?
> Detectar e resolver bugs mais rápido, melhorar a qualidade do software e reduzir o tempo para validar e lançar atualizações.

> [!question]- Qual era o problema do modelo antigo?
> Os devs trabalhavam isolados por longos períodos e só juntavam as mudanças no fim. O merge era complexo e demorado, os erros se acumulavam, e surgiam conflitos e atrasos.

> [!question]- O que garante a entrega (distribuição) contínua?
> Que as alterações sejam automaticamente preparadas e implementadas num ambiente de teste e/ou produção depois da compilação, com sempre um artefato validado e pronto para implantar.

> [!question]- Quais testes a entrega contínua automatiza, além dos de unidade?
> Testes de interface do usuário, carga, integração e confiabilidade de API.

## Aula 2 - Fundamentos
> [!question]- Onde ficam os arquivos de workflow?
> Na pasta `.github/workflows`, como arquivos `.yml` ou `.yaml`. Cada arquivo define uma única pipeline. → [[Workflows, Jobs, Steps e Actions]]

> [!question]- Workflow × job × step × action?
> Workflow: o pipeline de automação. Job: uma série de steps na mesma instância de runner. Step: um comando individual (shell ou ação). Action: o menor bloco de construção, um código reutilizável.

> [!question]- Quais eventos a aula cita?
> `push`, `pull_request` e `schedule`.

> [!question]- Jobs rodam sempre em sequência?
> Não. Podem rodar em paralelo ou em sequência, cada um no seu ambiente (máquina virtual), por exemplo um em Linux e outro em Windows.

> [!question]- Qual é a grande vantagem do GitHub Actions?
> A integração direta com o GitHub, sem precisar de uma ferramenta externa de CI/CD.

> [!question]- Onde ficam as ações personalizadas, e em que linguagem podem ser escritas?
> Em seus próprios repositórios, em qualquer linguagem que possa ser executada num runner.

> [!question]- Qual é o cuidado de segurança com ações de terceiros?
> Elas têm os mesmos privilégios do seu usuário e podem rodar código malicioso. Use fontes confiáveis e fixe numa versão específica.

> [!question]- Como otimizar o uso de minutos?
> Com a matriz de jobs (vários ambientes em paralelo) e ações de cache (instalar dependências mais rápido).

> [!question]- No exemplo de CI/CD da aula 2, o que acontece a cada push na branch principal?
> O GitHub Actions constrói o projeto, executa todos os testes e depois implanta o código no ambiente de produção, se todos os testes passarem. No YAML, o job `deploy` tem `needs: build`.

## Aula 3 - On-Premises e runners
> [!question]- O que é um ambiente On-Premises?
> Uma infraestrutura de TI mantida fisicamente dentro da organização, ao contrário da nuvem. "On-premises" significa "no local". → [[Ambiente On-Premises]]

> [!question]- Cite as vantagens e as desvantagens do On-Premises.
> Vantagens: controle total, segurança com políticas próprias e conformidade (dados armazenados localmente). Desvantagens: custo, escalabilidade limitada, e redundância e recuperação de desastres por conta da empresa.

> [!question]- O que são runners?
> Agentes que hospedam a execução dos jobs de um workflow. Podem ser hospedados pelo GitHub ou auto-hospedados. → [[Runners do GitHub Actions]]

> [!question]- Quando usar runners auto-hospedados?
> Para hardware ou software específicos, restrições de rede, mais controle, economia de custos, configuração personalizada e desempenho.

> [!question]- Cite boas práticas com runners auto-hospedados.
> Isolar workloads, manter atualizado, restringir o acesso (sem guardar segredos), monitoramento e logs, recuperação de desastres, reiniciar regularmente ou usar runners efêmeros, e gerenciar a capacidade.

> [!question]- Quais são os limites com runners auto-hospedados?
> Workflow até 35 dias, job até 24 h na fila, 1.000 requisições à API por hora por repositório, matriz até 256 jobs, 500 execuções em fila a cada 10 s por repositório e 10.000 runners por grupo.

## Aula 4 - Docker
> [!question]- Que problema clássico o Docker elimina?
> O "funciona na minha máquina", porque o app e as dependências encapsulados rodam igual em qualquer ambiente. → [[GHA 04 - Conceitos básicos de Docker]]

> [!question]- Por que os contêineres são eficientes em comparação com VMs?
> Porque compartilham o kernel do sistema operacional, mas mantêm processos e arquivos separados, sem o overhead de uma VM completa.

> [!question]- Imagem × contêiner?
> A imagem é o modelo estático (pacote leve e executável, com camadas). O contêiner é a instância executável: a imagem em tempo de execução.

> [!question]- Cite os casos de uso do Docker na aula 4.
> Desenvolvimento e teste, CI/CD, microsserviços e orquestração (com Kubernetes).

## Aula 5 - Repositórios de imagens
> [!question]- O que é um repositório de imagens Docker?
> Um local centralizado para armazenar, recuperar, compartilhar e gerenciar imagens, como uma biblioteca. → [[Repositórios de Imagens Docker]]

> [!question]- Que imagem o `docker pull` baixa se a tag não for especificada?
> A `latest`.

> [!question]- Quais comandos enviam uma imagem para o Docker Hub?
> `docker images` (identificar), `docker tag minha_imagem meu_usuario/nome_do_repositório:tag`, `docker login` e `docker push meu_usuario/nome_do_repositório:tag`.

> [!question]- Qual plataforma se integra ao ECS e ao Kubernetes e replica entre regiões?
> O Amazon ECR.

> [!question]- Qual plataforma é um repositório universal, para vários tipos de pacote?
> O JFrog Artifactory.

> [!question]- Para que serve assinar imagens?
> Para garantir integridade e autenticidade, permitindo verificar se a imagem foi alterada desde que foi criada.

> [!question]- Quais regulamentações a aula cita em compliance?
> GDPR, HIPAA e PCI-DSS.

## Dúvidas em aberto
- [ ] O resumo da aula 2 cita "habilidades avançadas" (implantação segura, integração com ferramentas externas), sem conteúdo no texto.
- [ ] A Figura 6 da aula 5 tem a legenda "Dashboard do ACR da AWS", mas está na seção do ECR.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
