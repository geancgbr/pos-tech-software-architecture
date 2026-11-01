---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Volume, Volumes, Container de dados, Containers de dados, Backup de volumes]
---

# Volumes e Containers de Dados

- **Backup de volumes**: uma cópia segura de um volume. Em caso de falha ou exclusão por engano, serve para criar um volume com os dados copiados.
- **Containers de dados**: separam os dados e permitem que **vários contêineres usem os mesmos dados**.
  - Nomeia-se um volume no contêiner de dados, e os outros o consomem.
  - A pasta é **criada automaticamente na raiz do Docker**: não é preciso um diretório persistente específico, porque toda conexão vai para o contêiner de dados.
  - **Exemplo**: um contêiner de dados com imagem **mysql** e volume **dadosdb**. Vale para quantos contêineres de dados forem necessários.
- **No Compose** (aula 3): o bloco **volume** cria discos (nome seguido de `:`), e a instrução **volumes** de um serviço aponta para um volume ou para pastas dentro dele.

Volumes no Kubernetes: [[Volumes, PV, PVC e StorageClass]].

Aparece em: [[DK 02 - Gerenciamento de contêineres]], [[DK 03 - Orquestração de contêineres]]
