---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Docker Desktop, WSL]
---

# Docker

Ferramenta **open source** lançada em **2013** pela **dotCloud** para melhorar o **isolamento e o uso de recursos** e rodar aplicações **sem interface gráfica**, em comparação com uma VM. Só é possível graças ao **isolamento de processos e à virtualização do Kernel Linux**. Junto do Kernel, duas tecnologias isolam os contêineres: [[Cgroups e Namespaces]].

**Peças principais**
- **[[Contêiner|Contêineres]]**: ambientes isolados onde as aplicações rodam.
- **[[Imagens Docker e Docker Hub|Imagens]]**: empacotam o SO, as dependências, as portas e as variáveis de ambiente, versionadas por **tags** e distribuídas pelo **Docker Hub**.
- **[[Dockerfile e Camadas (Layers)|Dockerfile]]**: as instruções da imagem.
- **[[Volumes e Containers de Dados|Volumes]]**: dados persistentes e compartilhados.
- **[[Docker Compose]]**: vários contêineres a partir de um `docker-compose.yml`.

**No Windows**: o **WSL** (subsistema Linux, distribuições como Ubuntu e Debian) mais o **Docker Desktop** integrado a ele. Os comandos Docker rodam no ambiente Linux.

**Segurança**: [[Trivy]]. **Na nuvem AWS**: [[ECS (Elastic Container Service)]].

**Onde o Docker aparece na Fase 1**: como ferramenta para criar o ambiente de testes de integração ([[QS 04 - Testes de integração]]) e nos containers do Hands On de monitoramento com Prometheus e Grafana ([[ARQ 04 - Escalabilidade, disponibilidade e desempenho]]).

## Na disciplina GitHub Actions (aula 4)
Uma **plataforma aberta** para criar, empacotar e executar aplicativos em contêineres. Resolve problemas de compatibilidade, dependências e diferenças entre ambientes, e acaba com o **"funciona na minha máquina"**. Casos de uso: desenvolvimento e teste · CI/CD · microsserviços · orquestração (Kubernetes). Impacto: padronização, agilidade, inovação, ecossistema e sustentabilidade. Instalação no Windows, no Mac e no Ubuntu (`docker-ce`): [[GHA 04 - Conceitos básicos de Docker]].

## Na disciplina Kubernetes (parte 1, aula 1)
Software de **plataforma aberta** que implementa contêineres, com **arquitetura cliente-servidor**, para data center, cloud ou ambiente híbrido. É pré-requisito do ambiente (validar com `docker -v`) e o mecanismo de virtualização do [[Minikube]]. → [[K8S1 01 - Introdução ao Kubernetes]]

Aparece em: [[DK 01 - Introdução ao Docker]] a [[DK 06 - ECS]], [[K8S1 01 - Introdução ao Kubernetes]]
