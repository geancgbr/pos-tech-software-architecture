---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Dockerfile, Layers, Camadas Docker, Multistage, ARG, ENV]
---

# Dockerfile e Camadas (Layers)

**Dockerfile**: o arquivo onde se declaram os comandos, as instalações, as variáveis e as portas de uma imagem personalizada. **O nome do arquivo já é a sua extensão.** O PDF mostra um exemplo simples e um **multistage** (aula 1, Figuras 5 e 6).

**Layers** (aula 4)
- **Uma camada por instrução**. O **`FROM`** é a **camada zero**.
- **A camada de baixo depende da camada de cima.**
- **Cache**: as camadas antes da que mudou vêm do cache, e todas as seguintes são **recriadas**. No exemplo, o build caiu de cerca de 55 s para cerca de 15 s.
- **Boa prática**: as camadas devem ser pensadas para obter essa estrutura, o que facilita e agiliza os testes e o desenvolvimento local.
- O uso do cache também se aplica aos repositórios on-line: Docker Hub, AWS ECR, Azure Container Registry e Google Cloud Container Registry.

**ARG com ENV** (aula 4): passe valores no **build** (`build-arg`) para **não expor valores sensíveis** no Dockerfile, e use-os junto com a instrução **ENV**.

**No Compose** (aula 3): `command` e `entrypoint` **substituem** o CMD e o ENTRYPOINT da imagem ou do Dockerfile, e a instrução `build` "builda" a imagem a partir de um Dockerfile, cujo local é definido pelo contexto.

Aparece em: [[DK 01 - Introdução ao Docker]], [[DK 03 - Orquestração de contêineres]], [[DK 04 - Melhores práticas e solução de problemas]]
