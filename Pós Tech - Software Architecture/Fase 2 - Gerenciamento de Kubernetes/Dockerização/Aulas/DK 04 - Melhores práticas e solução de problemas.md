---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 4
fonte: "Aula 04- Melhores Práticas e Solução de Problemas.pdf"
---

# DK 04 - Melhores práticas e solução de problemas

← [[DK 03 - Orquestração de contêineres]] · [[Dockerização]] · Próxima → [[DK 05 - Segurança de contêineres]]

> [!summary] Em uma frase
> Toda imagem tem **camadas (layers)**, uma por instrução do Dockerfile. Organizá-las bem permite **reaproveitar o cache** e acelerar o build. Outra boa prática é usar **ARG** (com ENV) para **não expor valores sensíveis** no Dockerfile. Veja [[Dockerfile e Camadas (Layers)]].

## Hands On
Boas práticas na criação de imagens, solução de problemas comuns e as camadas ("layers") de uma imagem, usadas a favor das alterações.

## Layers (camadas)
- **Uma camada = uma instrução** no Dockerfile. Cada instrução nova cria uma camada adicional.
- A instrução **`FROM`** é a **camada zero**.
- As camadas seguem um fluxo comum: **a camada de baixo depende da camada de cima**, e assim por diante.
- **Exemplo da aula** (Figura 1): um Dockerfile com **7 camadas**.

## Cache entre builds
- Num novo build, as camadas **antes** da que mudou vêm do **cache**. A partir da camada alterada, **todas as seguintes são recriadas do zero**.
- **Exemplo**: um arquivo novo na raiz do projeto altera a camada **`COPY`** (linha 9). As anteriores vêm do cache, e as seguintes são refeitas.
- **Resultado**: o primeiro build levou cerca de **55 segundos**, e o build com cache, cerca de **15 segundos** (Figuras 2 e 3).
- Por isso, **as camadas devem ser pensadas** para essa estrutura, facilitando e agilizando os testes e o desenvolvimento local.
- O cache também vale nos **repositórios on-line**: Docker Hub, **AWS ECR**, **Azure Container Registry** e **Google Cloud Container Registry**.
- O Docker Hub mostra os layers de uma imagem, como a do **node** (Figura 6).

## ARG com ENV
- Boa prática para **não expor valores sensíveis** num Dockerfile.
- Os argumentos são passados **no momento do build** e entram como valor do argumento definido no Dockerfile. Podem ser usados junto com a instrução **ENV**.
- O exemplo está nas Figuras 4 (Dockerfile com ARG e ENV) e 5 (o `build-arg`) do PDF.

> [!note] O título e a introdução da aula falam em "problemas comuns que o Docker e o Docker Compose podem apresentar e como solucioná-los" e em "casos de uso avançado", mas o texto do PDF trata só de **layers** e de **ARG/ENV**, como confirma o resumo final da própria aula.

## Referências
Barancelli, *Boas práticas para criar imagens Docker eficientes, seguras e escaláveis* (2023) · Docker Hub, *Node Tags and Layers*
