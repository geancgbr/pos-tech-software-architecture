---
tags: [pos-tech/fase-2, github-actions, aula]
disciplina: GitHub Actions
aula: 5
fonte: "Aula 05 - Repositório de imagens Docker.pdf"
---

# GHA 05 - Repositório de imagens Docker

← [[GHA 04 - Conceitos básicos de Docker]] · [[GitHub Actions]]

> [!summary] Em uma frase
> Um [[Repositórios de Imagens Docker|repositório de imagens Docker]] é um **local centralizado para armazenar, recuperar, compartilhar e gerenciar imagens**, como uma biblioteca. O Docker Hub é o padrão. Há também GCR, ECR, ACR, GitLab Container Registry, Quay e JFrog Artifactory, e a segurança deve ser prioridade.

## Hands On: Docker Hub na prática
O **Docker Hub** é um serviço de nuvem para compartilhar e acessar imagens com a comunidade e a equipe, "um **GitHub para imagens Docker**".

1. **Criar conta**: acessar o Docker Hub, clicar em **"Register"** e seguir as instruções.
2. **Procurar imagens**: buscar pelo nome (ex.: `nginx`, `node`) e observar as **descrições e a quantidade de downloads** (sinal de popularidade e confiabilidade).
3. **Baixar**: sem tag, baixa a `latest`.
   ```bash
   docker pull nome_da_imagem:tag
   docker pull nginx:latest
   ```
4. **Criar um repositório**: fazer login, clicar em **"Create Repository"**, dar um nome e definir a visibilidade (**público ou privado**).
5. **Enviar a sua imagem**:
   ```bash
   docker images                                                   # identificar a imagem
   docker tag minha_imagem meu_usuario/nome_do_repositório:tag     # renomear no formato do Docker Hub
   docker login                                                    # login pelo terminal
   docker push meu_usuario/nome_do_repositório:tag                 # enviar
   ```
6. **Gerenciar**: editar descrições, configurar **webhooks** para automatizar fluxos, excluir ou atualizar imagens.

## Repositório de imagens
- **Local de armazenamento centralizado** de imagens. É o ponto de intersecção entre devs, administradores e outros stakeholders.
- **Analogia**: uma **biblioteca**, com imagens oficiais (de fornecedores conhecidos) e da comunidade.
- **Funções**: armazenamento · recuperação · compartilhamento · gerenciamento (versões, atualizações, manutenção).
- **Tipos**: **públicos** (qualquer pessoa; imagens gratuitas e de código aberto) e **privados** (só autorizados; mais segurança e personalização).
- As plataformas oferecem busca rápida, controle de versão, segurança e integração com ferramentas DevOps, e variam em recursos, escalabilidade, compatibilidade e preço.

## Plataformas
| Plataforma | Descrição | Recursos |
|---|---|---|
| **Docker Hub** | O repositório **padrão** do Docker, público ou privado | Busca, armazenamento, compartilhamento, **varredura de segurança**, integração com CI/CD |
| **Google Container Registry (GCR)** | Google Cloud, otimizado para desempenho e segurança | Integração nativa com o Google Cloud, **IAM**, repositórios privados |
| **Amazon Elastic Container Registry (ECR)** | Serviço gerenciado da AWS | Integração com **Amazon ECS e Kubernetes**, políticas de segurança, **replicação entre regiões** |
| **Azure Container Registry (ACR)** | Microsoft Azure, para todos os tipos de implantação | Docker CLI e API, integração com **Azure DevOps**, autenticação avançada |
| **GitLab Container Registry** | Integrado ao GitLab | **CI/CD do GitLab**, repositórios privados, automação |
| **Quay by Red Hat** | Solução empresarial de segurança e automação | **Varredura automatizada**, controle de acesso granular, vários protocolos de registro |
| **JFrog Artifactory** | Repositório **universal**, para todos os principais pacotes, inclusive Docker | Vários repositórios, controle de acesso, CI/CD, análise |

> [!note] A Figura 6 do PDF tem a legenda "Dashboard do ACR da AWS", mas está na seção do **ECR** (o ACR é o serviço da Azure).

## Considerações de segurança
| Aspecto | O que fazer |
|---|---|
| **Varredura de vulnerabilidades** | Escanear as imagens regularmente, com ferramentas automatizadas |
| **Assinatura e verificação** | Assinar digitalmente, para garantir integridade e autenticidade (se a imagem foi alterada desde a criação) |
| **Controle de acesso** | Políticas rigorosas: só autorizados baixam, carregam ou modificam imagens em repositórios privados |
| **Políticas personalizadas** | Padrões de conformidade, restrições de rede, autenticação de dois fatores |
| **Registros e monitoramento** | Logs detalhados e monitoramento em tempo real, para detectar atividades suspeitas |
| **Atualizações e patches** | Manter as imagens com as últimas correções de fornecedores confiáveis |
| **Compliance e auditorias** | Seguir padrões como **GDPR, HIPAA, PCI-DSS**, com auditorias internas e externas |
| **Educação e conscientização** | Treinar a equipe sobre boas práticas e ameaças emergentes |

A segurança combina **tecnologia, processos e cultura organizacional**.

## Referências
AWS (ECR) · Azure (ACR) · Docker Hub · GitLab (Container Registry) · Google Cloud (Artifact Registry) · Red Hat (Quay)
