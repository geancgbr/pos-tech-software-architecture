---
tags: [pos-tech/fase-2, github-actions, aula]
disciplina: GitHub Actions
aula: 2
fonte: "Aula 02 - Fundamentos básicos.pdf"
---

# GHA 02 - Fundamentos básicos

← [[GHA 01 - Introdução]] · [[GitHub Actions]] · Próxima → [[GHA 03 - GitHub Actions em ambientes On-Premises]]

> [!summary] Em uma frase
> Os conceitos centrais são **[[Workflows, Jobs, Steps e Actions]]**, mais os **triggers (eventos)**. Um workflow é um arquivo `.yml` em `.github/workflows`, com jobs que rodam em **runners**, e cada job tem steps que executam comandos ou **actions** reutilizáveis.

## Hands On: o primeiro pipeline
1. Crie um repositório novo no GitHub e clone-o com `git clone`.
2. Na raiz, crie a pasta **`.github/workflows`** e, dentro dela, o arquivo **`ci-cd.yml`**:

```yaml
name: CI/CD Pipeline
on:
  push:
    branches:
      - main
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
```

3. Envie com `git add`, `git commit` e `git push`.
4. No repositório, abra a aba **"Actions"**: o fluxo CI/CD deve aparecer em execução.

## O que é
- Ferramenta de automação para **criar, testar e implantar** aplicativos direto do GitHub, uma solução completa de CI/CD.
- Configura **"actions" em resposta a eventos** (push, pull request). Uma ação é um **pedaço reutilizável de código** que executa um job (build, testes). Ações se combinam em **"workflows"**.
- **Grande vantagem**: a **integração direta com o GitHub**, sem precisar de ferramenta externa de CI/CD. É **flexível e personalizável**: ações predefinidas do GitHub ou da comunidade, ou ações próprias.

## Os conceitos principais
| Conceito | O que é |
|---|---|
| **Workflows** | Os pipelines de automação do repositório. São compostos por **um ou mais jobs** e dizem **quando e em que circunstâncias** rodar |
| **Triggers** (eventos) | Atividades que **acionam** o workflow: push, pull request, um cronograma |
| **Jobs** | As partes do workflow: uma **série de passos executados na mesma instância de runner** |
| **Steps** | Os comandos individuais de um job. Cada um executa uma única ação (ou um script) |
| **Actions** | O **menor bloco de construção**: um pedaço de código **reutilizável** que um step executa |

O fluxo de steps está na Figura 1 do PDF.

### Workflows e eventos
- Ficam em arquivos **`.yml` ou `.yaml`** na pasta **`.github/workflows`**. **Cada arquivo define uma única pipeline.**

```yaml
name: Meu primeiro fluxo de trabalho
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
```
Esse workflow roda a cada **push**. O job **build** roda no Ubuntu mais recente, com um step que faz o checkout via `actions/checkout@v2`.

**Eventos**: **`push`** (a cada push) · **`pull_request`** (a cada pull request aberta) · **`schedule`** (num cronograma, ex.: todo dia à meia-noite). Um workflow pode ter um ou mais:

```yaml
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
```

### Jobs
- Cada job é **uma fase do pipeline**, com um ou mais passos na **mesma instância do runner**.
- Vários jobs rodam **em paralelo ou em sequência**.
- Cada job tem **seu próprio ambiente** e roda de forma independente **na sua máquina virtual**. Por exemplo, um em Linux e outro em Windows:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
  test:
    runs-on: windows-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Run tests
        run: dotnet test
```

### Steps
Executam **comandos shell** ou **ações**:
```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v2
  - name: Install dependencies
    run: npm install
  - name: Run tests
    run: npm test
```

### Actions
- **O menor bloco de construção.** Encapsulam sequências de comandos (checkout, instalar dependências, rodar testes) ou ações complexas que interagem com outros serviços.
- Há **muitas ações predefinidas** do GitHub e da comunidade. Exemplo: `actions/checkout@v2` faz checkout do código para o runner.
- São **reutilizáveis** entre workflows e repositórios e podem ser compartilhadas com a comunidade.
- **Ações personalizadas** ficam **em seus próprios repositórios** e podem ser escritas em **qualquer linguagem que rode num runner**.

## Aplicações práticas
**CI/CD**: build, testes e deploy em produção se os testes passarem:
```yaml
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Build
        run: make
      - name: Test
        run: make test
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        run: make deploy
```

**Automação de issues e pull requests**: adicionar etiquetas a novas issues, fechar PRs sem atividade há um tempo.

## Boas práticas
| Prática | O que fazer |
|---|---|
| **Segurança** | Cuidado com ações de terceiros: **têm os mesmos privilégios do seu usuário** e podem rodar código malicioso. Use **fontes confiáveis** e **fixe numa versão específica** |
| **Otimização de recursos** | Os **minutos são limitados**. Use a **matriz de jobs** (testar em vários ambientes em paralelo) e **ações de cache** (instalar dependências mais rápido) |
| **Documentação** | Comente e descreva o que cada workflow faz |

> [!note] O resumo final fala em "habilidades avançadas" (implantação segura, integração com ferramentas externas), mas o texto do PDF não detalha esses temas.

## Referências
GitHub Docs: criar ações, ação de contêiner Docker, documentação, Entendendo o GitHub Actions, eventos, fortalecimento de segurança, jobs, steps, sintaxe, fluxos de trabalho (matriz) · GitHub Marketplace (Actions)
