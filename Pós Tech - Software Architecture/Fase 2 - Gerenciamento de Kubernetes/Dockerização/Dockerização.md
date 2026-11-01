---
tags: [pos-tech/fase-2, docker, indice]
disciplina: Dockerização
fase: 2
aulas: 6
---

# Dockerização

[[Fase 2 - Gerenciamento de Kubernetes]] · Revisão → [[Revisão - Dockerização]]

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[DK 01 - Introdução ao Docker]] | [[Docker]], [[Contêiner]], [[Cgroups e Namespaces]], [[Imagens Docker e Docker Hub]] |
| 2 | [[DK 02 - Gerenciamento de contêineres]] | [[Contêiner]], [[Volumes e Containers de Dados]], [[Imagens Docker e Docker Hub]] |
| 3 | [[DK 03 - Orquestração de contêineres]] | [[Docker Compose]] |
| 4 | [[DK 04 - Melhores práticas e solução de problemas]] | [[Dockerfile e Camadas (Layers)]] |
| 5 | [[DK 05 - Segurança de contêineres]] | [[Trivy]] |
| 6 | [[DK 06 - ECS]] | [[ECS (Elastic Container Service)]] |

## Comandos que estão no texto dos PDFs
| Para quê | Comando |
|---|---|
| Listar contêineres, inclusive parados | `docker container ls -a` |
| Limitar CPU e memória na criação | `--cpus=1` e `-m 512m` no `docker container run` |
| Conferir a configuração | `docker container inspect` + `grep` (cpu, mem) |
| Alterar recursos em execução | `docker container update` |
| Subir, buildar, logs, listar, escalar, parar e remover (Compose) | `docker compose up`, `build`, `logs`, `ps`, `scale`, `start`, `stop`, `restart`, `down` |
| Scan de vulnerabilidades | `trivy image teste-trivy:latest` · `trivy image --severity CRITICAL,HIGH teste-trivy:latest` |

## Material
PDFs em `~/Desktop/Dockerização/`. **As notas resumem apenas o conteúdo escrito nos PDFs.** Muitos exemplos estão **só em imagem** e não aparecem nas notas: os Dockerfiles simples e multistage, os comandos de `run`, `inspect`, `update` e do container de dados, o `docker-compose.yml` do Kong, o Dockerfile de layers, ARG/ENV e as saídas do Trivy. Quando uma nota cita uma figura, consulte o PDF.

## Referências
Microsoft Learn (WSL) · ETCD.DEV (namespaces e cgroups) · Red Hat (Kernel Linux) · Stack.desenvolvedor.expert (rede e armazenamento) · Docker Docs (Compose) · Baeldung (restart policies) · 4Linux (Compose) · Barancelli (boas práticas) · Docker Hub (node) · Aqua Vulnerability Database · TrendMicro · Medium (Trivy) · Trivy Docs · Alura (EC2 × ECS) · AWS (CPU no ECS) · Ilegra (ECS)
