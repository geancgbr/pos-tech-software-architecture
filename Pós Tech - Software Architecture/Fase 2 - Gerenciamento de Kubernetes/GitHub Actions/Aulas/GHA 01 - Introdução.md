---
tags: [pos-tech/fase-2, github-actions, aula]
disciplina: GitHub Actions
aula: 1
fonte: "Aula 01 - Introdução.pdf"
---

# GHA 01 - Introdução

[[GitHub Actions]] · Próxima → [[GHA 02 - Fundamentos básicos]]

> [!summary] Em uma frase
> O **GitHub Actions** é a plataforma de automação do GitHub, **lançada em 2018** e incorporada ao gerenciamento de repositórios, para criar, personalizar e executar **pipelines de CI/CD**. A aula também revisa o que são **integração contínua** e **entrega (distribuição) contínua**.

## Hands On (vídeos)
Criação de uma conta no GitHub:
1. Visitar o site do GitHub.
2. Clicar em **"Sign up"**, no canto superior direito.
3. Preencher as informações (nome de usuário, e-mail e senha).
4. Confirmar que não é um robô.
5. Escolher o plano (o **gratuito** é suficiente para muitos iniciantes).
6. Configurar o perfil (opcional).
7. **Verificar o e-mail**, clicando no link enviado pelo GitHub.

O PDF traz as Figuras 1 e 2 ("arquitetura tradicional × virtualizada"), sem explicação no texto.

## GitHub Actions
- Plataforma de automação desenvolvida pelo GitHub e **incorporada ao sistema de gerenciamento de repositórios**.
- **Lançada em 2018.** Cria, personaliza e executa pipelines de CI/CD numa interface familiar.
- Facilita o desenvolvimento, o teste e a implantação, para que os devs tenham **mais tempo para criar software de qualidade**.
- O fluxo está na Figura 3 do PDF.

## Integração contínua
- Método fundamental, especialmente no **DevOps**: os devs combinam regularmente suas alterações num **repositório central**. Depois disso, **compilações são criadas e testes são executados**.
- Não é só a etapa de compilação ou integração. Tem um **componente de automação** (uma ferramenta de CI ou um serviço de compilação) e um **componente cultural** (a mentalidade de integrar com frequência).
- **Objetivos**: detectar e resolver bugs mais rápido, melhorar a qualidade e reduzir o tempo para validar e lançar atualizações.
- **Como era antes**: os devs trabalhavam **isolados por longos períodos** e só juntavam as mudanças à ramificação mestre no fim. O merge era complexo e demorado, os erros se acumulavam, havia conflitos e os lançamentos atrasavam.
- **Hoje**: confirmações frequentes num repositório compartilhado, com um **controle de versão como o Git**.
  - Antes de cada confirmação, é comum o dev rodar **testes de unidade locais**.
  - Um **serviço de CI** cria e executa os testes de unidade automaticamente a cada alteração.

## Entrega contínua (distribuição contínua)
- É uma **evolução lógica** da CI: as alterações de código são **automaticamente preparadas para produção**.
- Garante que as alterações sejam **implementadas automaticamente num ambiente de teste e/ou de produção** depois da compilação, de modo que sempre haja **um artefato de compilação validado e pronto para implantação**.
- **Automatiza vários testes** além dos de unidade: **interface do usuário, carga, integração, confiabilidade de API**.
- A **computação em nuvem** tornou mais fácil e barato criar e replicar ambientes de teste.

**Leituras recomendadas**: *GitHub Actions documentation*, *Understanding GitHub Actions*, *Workflow syntax for GitHub Actions* e os textos da AWS "O que significa integração contínua?" e "O que significa distribuição contínua?".

## Referências
AWS (distribuição contínua; integração contínua) · GitHub (Actions) · GitHub Docs (documentação, Understanding, Workflow syntax) · Walter, *5 dicas para aplicar DevOps* (2020)
