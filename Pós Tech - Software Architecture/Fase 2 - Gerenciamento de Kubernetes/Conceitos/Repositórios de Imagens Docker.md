---
tags: [pos-tech/fase-2, github-actions, docker, conceito]
aliases: [Repositório de imagens, Registry, Container Registry, ECR, ACR, GCR, Quay, JFrog Artifactory, GitLab Container Registry]
---

# Repositórios de Imagens Docker

**Local centralizado para armazenar, recuperar, compartilhar e gerenciar imagens Docker**, como uma biblioteca (aula 5 de GitHub Actions).

- **Funções**: armazenamento · recuperação · compartilhamento · gerenciamento.
- **Tipos**: públicos (gratuitos e abertos) e privados (restritos, mais segurança).
- **Plataformas**: Docker Hub (padrão, com varredura de segurança) · Google Container Registry (Google Cloud, IAM) · Amazon ECR (ECS, Kubernetes, replicação entre regiões) · Azure Container Registry (Azure DevOps) · GitLab Container Registry (CI/CD do GitLab) · Quay by Red Hat (varredura automatizada, acesso granular) · JFrog Artifactory (universal).
- **Segurança**: varredura de vulnerabilidades · assinatura e verificação · controle de acesso · políticas personalizadas · logs e monitoramento · patches · compliance (GDPR, HIPAA, PCI-DSS) · educação.
- **Comandos do Docker Hub**: `docker pull`, `docker images`, `docker tag`, `docker login`, `docker push`.

**Na disciplina Dockerização**: o cache de camadas também vale no Docker Hub, AWS ECR, Azure Container Registry e Google Cloud Container Registry ([[Dockerfile e Camadas (Layers)]]), e o Docker Hub é tratado em [[Imagens Docker e Docker Hub]].

## Na disciplina Desenvolvimento Serverless (Fase 3)
Publicar no **ECR** com o AWS CLI: `aws ecr create-repository`, `aws ecr get-login-password | docker login`, `docker tag` e `docker push` para a URL do registry ([[SLS 03 - ECS Fargate e ECR]]).

Aparece em: [[GHA 05 - Repositório de imagens Docker]], [[SLS 03 - ECS Fargate e ECR]]
