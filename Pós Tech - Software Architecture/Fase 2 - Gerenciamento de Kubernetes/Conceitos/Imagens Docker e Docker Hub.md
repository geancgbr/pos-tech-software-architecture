---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Imagem Docker, Imagens Docker, Docker Hub, Tags Docker, latest, Alpine]
---

# Imagens Docker e Docker Hub

**Imagem**: empacota o **sistema operacional, as dependências, as portas expostas e as variáveis de ambiente** (aula 1). No ECS (aula 6), as imagens são "instantâneos" da aplicação, com código, runtime, bibliotecas e configurações.

**Tags**: definem a **versão da imagem**, para controle, atualização e organização (bugs, melhorias, segurança). A mais recente é sempre a **`latest`**, e há variações, como uma latest com Windows Server Core (aula 2).

**Docker Hub**: "um GitHub voltado para imagens Docker". Tem imagens **oficiais** e **não oficiais**, públicas ou privadas, baixadas com **pull** (URL + tag). Na busca aparecem imagens **oficiais, verificadas pelo Publisher e patrocinadas**. **Cuidado com imagens suspeitas.**

**Registros na nuvem citados** (aula 4): AWS ECR, Azure Container Registry, Google Cloud Container Registry. O cache de camadas também vale neles.

**Imagens enxutas** (aula 5): bases com menos pacotes **reduzem as vulnerabilidades**. A imagem do Node 18 na variação **alpine** é bem menor e não teve nenhuma vulnerabilidade no scan com [[Trivy]].

## Na disciplina GitHub Actions (aulas 4 e 5)
- **Imagem**: pacote leve, autônomo e executável (código, bibliotecas, variáveis, configurações). É o **modelo estático** a partir do qual os contêineres são criados, com **camadas** (uma por instrução do Dockerfile) que podem ser compartilhadas entre imagens.
- **Docker Hub**: serviço de nuvem, "um GitHub para imagens Docker". `docker pull nome:tag` (sem tag, baixa a `latest`), "Create Repository" (público ou privado), `docker tag`, `docker login` e `docker push`, além de webhooks. Ao buscar, observe a descrição e o número de downloads.
- Outras plataformas e segurança: [[Repositórios de Imagens Docker]].

Aparece em: [[DK 01 - Introdução ao Docker]], [[DK 02 - Gerenciamento de contêineres]], [[DK 04 - Melhores práticas e solução de problemas]], [[DK 05 - Segurança de contêineres]]
