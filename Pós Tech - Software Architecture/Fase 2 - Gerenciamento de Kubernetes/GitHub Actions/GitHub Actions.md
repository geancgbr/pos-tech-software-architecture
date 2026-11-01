---
tags: [pos-tech/fase-2, github-actions, indice]
disciplina: GitHub Actions
fase: 2
aulas: 5
---

# GitHub Actions

[[Fase 2 - Gerenciamento de Kubernetes]] · Revisão → [[Revisão - GitHub Actions]]

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[GHA 01 - Introdução]] | [[Integração Contínua (CI)]], [[Entrega Contínua e Deploy Contínuo]] |
| 2 | [[GHA 02 - Fundamentos básicos]] | [[Workflows, Jobs, Steps e Actions]] |
| 3 | [[GHA 03 - GitHub Actions em ambientes On-Premises]] | [[Ambiente On-Premises]], [[Runners do GitHub Actions]] |
| 4 | [[GHA 04 - Conceitos básicos de Docker]] | [[Docker]], [[Contêiner]], [[Imagens Docker e Docker Hub]] |
| 5 | [[GHA 05 - Repositório de imagens Docker]] | [[Repositórios de Imagens Docker]] |

## Anatomia de um workflow
```text
.github/workflows/ci-cd.yml   → 1 arquivo = 1 workflow (pipeline)
  on:        → triggers (push, pull_request, schedule)
  jobs:      → 1+ jobs, cada um em sua VM/runner (runs-on), em paralelo ou em sequência
    steps:   → comandos (run:) ou actions reutilizáveis (uses: actions/checkout@v2)
```

## Ligações com outras disciplinas
- **DevOps (IaC and CI/CD)**: os Hands On das aulas 2 e 3 usam o GitHub Actions ([[DEV 03 - Testes automatizados com CI]]).
- **Dockerização**: as aulas 4 e 5 retomam [[Docker]], [[Contêiner]] e [[Imagens Docker e Docker Hub]].

## Material
PDFs em `~/Desktop/Github Actions/`. **As notas resumem apenas o conteúdo escrito nos PDFs.** O YAML e os comandos foram transcritos do texto. As figuras (arquitetura tradicional × virtualizada, fluxos, telas do Docker Hub, do ECR e do ACR) não estão nas notas.

## Referências
GitHub Docs · GitHub Marketplace · AWS (CI, CD, Docker, ECR) · Walter (2020) · Docker · Microsoft · Red Hat (Docker, Quay) · Azure (ACR) · GitLab · Google Cloud (Artifact Registry)
