---
tags: [pos-tech/fase-2, github-actions, conceito]
aliases: [Workflow, Workflows do GitHub Actions, Job, Jobs, Step, Steps, Action, Actions, Triggers, Eventos do GitHub Actions, ci-cd.yml]
---

# Workflows, Jobs, Steps e Actions

Os conceitos centrais do GitHub Actions (aula 2):

| Conceito | O que é | Detalhe |
|---|---|---|
| **Workflow** | O pipeline de automação | Arquivo `.yml`/`.yaml` em **`.github/workflows`**; **um arquivo = uma pipeline**; um ou mais jobs |
| **Trigger** (evento) | O que aciona o workflow | `push`, `pull_request`, `schedule` (cronograma); um ou mais por workflow |
| **Job** | Uma fase do pipeline | Uma série de steps na **mesma instância de runner**; roda **em paralelo ou em sequência**, em **sua própria VM** (ex.: `ubuntu-latest` e `windows-latest`). No exemplo de deploy da aula, o job `deploy` traz `needs: build` |
| **Step** | Um comando individual de um job | Executa um **comando shell** ou uma **ação**. No exemplo, o step com `uses: actions/checkout@v2` usa a ação, e o com `run: npm install` executa o comando |
| **Action** | O **menor bloco de construção** | Código **reutilizável** (ex.: `actions/checkout@v2`); predefinidas (GitHub e comunidade) ou personalizadas (num repositório próprio, em qualquer linguagem que rode no runner) |

**Boas práticas**: **segurança** (ações de terceiros têm os privilégios do seu usuário: use fontes confiáveis e **fixe a versão**) · **otimização** (minutos limitados: **matriz de jobs** e **cache**) · **documentação**.

**Aplicações**: CI/CD (build → test → deploy) e automação de issues e pull requests.

Exemplos YAML: [[GHA 02 - Fundamentos básicos]] · Na disciplina DevOps: [[DEV 03 - Testes automatizados com CI#Pipeline de testes]]

Aparece em: [[GHA 02 - Fundamentos básicos]]
