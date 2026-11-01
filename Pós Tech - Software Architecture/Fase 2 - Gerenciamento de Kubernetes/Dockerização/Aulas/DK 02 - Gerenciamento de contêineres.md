---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 2
fonte: "Aula 02- Gerenciamento de Contêineres.pdf"
---

# DK 02 - Gerenciamento de contêineres

← [[DK 01 - Introdução ao Docker]] · [[Dockerização]] · Próxima → [[DK 03 - Orquestração de contêineres]]

> [!summary] Em uma frase
> Como listar e inspecionar contêineres, **limitar e alterar CPU e memória sem derrubar o contêiner**, fazer backup de volumes, usar **[[Volumes e Containers de Dados|containers de dados]]** para compartilhar dados entre contêineres e escolher com cuidado as imagens no **Docker Hub**.

## Hands On
Comandos Linux e Docker para criar imagem, contêiner e volumes; logs de uma aplicação na prática; e a primeira aplicação **NodeJS** rodando num contêiner e acessada pela Web.

## `docker container ls -a`
O comando **`docker container`** mostra informações sobre os contêineres, inclusive os que já pararam. As colunas da saída (Figura 1):

| Coluna | Significado |
|---|---|
| **CONTAINER ID** | ID do contêiner, **único** para cada um |
| **IMAGE** | A imagem usada para executar o contêiner |
| **COMMAND** | O comando em execução |
| **CREATED** | Quando foi criado |
| **STATUS** | O status atual |
| **PORTS** | A porta do contêiner e a do host que ele usa |
| **NAMES** | O nome do contêiner |

## CPU e memória
- **Na criação**: para 1 CPU e 512 MB, adicione **`--cpus=1`** (CPU) e **`-m 512m`** (RAM) no `docker container run` (Figura 2).
- **Conferir**: pegue o ID com `docker container ls` e faça um **`inspect`** com **`grep`**, buscando "cpu" ou "mem" (Figura 3).
- **Alterar em execução**: use **`update`** (Figura 4). **O contêiner não precisa morrer** para aumentar os recursos. Vale para **RAM e CPU**.

## Volumes
- **Backup de volumes**: garante uma cópia segura. Em caso de falha ou exclusão por engano, o backup serve para criar um volume com os dados copiados.
- **Containers de dados**: separam os dados e permitem que **vários contêineres se comuniquem com os mesmos dados**.
  - Nomeia-se um volume dentro desse contêiner, que será consumido pelos outros.
  - Não é preciso criar um diretório persistente específico: a pasta é **criada automaticamente na raiz do Docker**, e toda conexão vai para o contêiner de dados, não para o diretório.
  - **Exemplo da aula** (Figuras 5 e 6): um contêiner de dados com imagem **mysql** e volume **dadosdb**, que outros contêineres podem ver e editar. Vale para quantos contêineres de dados forem necessários.

Veja [[Volumes e Containers de Dados]].

## Escolhendo imagens no Docker Hub
- Navegue até o Docker Hub, ou pesquise no Google o nome da imagem base + "Docker Hub" (ex.: Python, Figura 7).
- Na página oficial, a aba **"Tags"** lista todas as versões oficiais.
- A versão mais recente é sempre a **"latest"**. Além das versões padrão (ex.: 3.8, 3.7), há variações, como uma "latest" com **Windows Server Core** como imagem base (Figura 9).
- A busca no Docker Hub traz imagens **oficiais**, **verificadas pelo Publisher** e **patrocinadas**.

> [!warning] Cuidado
> Pode haver **imagens suspeitas** nos resultados. "Escolha com sabedoria!"

## Referências
Red Hat, *O que é Kernel Linux* (2019) · Stack.desenvolvedor.expert, *Entendendo a rede no Docker* e *Entendendo o armazenamento no Docker*
