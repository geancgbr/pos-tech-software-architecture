---
tags: [pos-tech/fase-2, docker, revisao]
disciplina: Dockerização
---

# Revisão - Dockerização

[[Dockerização]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- Quando e por quem o Docker foi lançado, e com que objetivo?
> Em 2013, pela dotCloud, como ferramenta open source para melhorar o isolamento e o uso de recursos e rodar aplicações sem interface gráfica, em comparação com uma VM. → [[Docker]]

> [!question]- Que funcionalidades do Kernel Linux tornam o Docker possível?
> O isolamento de processos e a virtualização.

> [!question]- Quais são as principais funções do Kernel Linux?
> Gerenciar memória, processos, drives, chamadas do sistema e segurança. → [[Cgroups e Namespaces]]

> [!question]- Cgroups × Namespaces?
> Cgroups: definem limites de uso de recursos (CPU, memória) dos processos. Namespaces: criam o isolamento, com cada contêiner tendo seus próprios usuários, rede, disco etc.

> [!question]- O que acontece com os outros contêineres se um deles quebrar (ex.: 100% de CPU)?
> Nada: graças aos Namespaces, eles não são afetados. É a analogia do navio cargueiro, em que o navio representa o host. → [[Contêiner]]

> [!question]- O que uma imagem Docker empacota?
> O sistema operacional, as dependências, as portas expostas e as variáveis de ambiente. → [[Imagens Docker e Docker Hub]]

> [!question]- O que é o Docker Hub?
> "Um GitHub voltado para imagens Docker": imagens oficiais e não oficiais, públicas ou privadas, baixadas com pull pela URL e pela tag.

> [!question]- Para que servem as tags?
> Para definir a versão da imagem (controle, atualização, organização, correções de bugs e de segurança).

> [!question]- Qual é a extensão do Dockerfile?
> Segundo a apostila, o nome do arquivo ("Dockerfile") já é a sua extensão. → [[Dockerfile e Camadas (Layers)]]

## Aula 2 - Gerenciamento
> [!question]- Que comando lista os contêineres, inclusive os parados?
> `docker container ls -a`. → [[DK 02 - Gerenciamento de contêineres]]

> [!question]- Cite as colunas da saída do `docker container ls`.
> CONTAINER ID, IMAGE, COMMAND, CREATED, STATUS, PORTS e NAMES.

> [!question]- Como criar um contêiner com 1 CPU e 512 MB de RAM?
> Adicionando as flags `--cpus=1` e `-m 512m`.

> [!question]- Como aumentar os recursos de um contêiner em execução?
> Com `update`, sem precisar derrubar o contêiner. Vale para RAM e CPU.

> [!question]- Para que serve um container de dados?
> Para separar os dados e permitir que vários contêineres usem os mesmos dados. O volume é nomeado nele e consumido pelos outros, e a pasta é criada automaticamente na raiz do Docker. → [[Volumes e Containers de Dados]]

> [!question]- Qual é a tag da versão mais recente de uma imagem?
> `latest`.

> [!question]- Que cuidado tomar ao buscar imagens no Docker Hub?
> Pode haver imagens suspeitas nos resultados. A busca traz imagens oficiais, verificadas pelo Publisher e patrocinadas.

## Aula 3 - Docker Compose
> [!question]- Qual é o papel do Docker Compose?
> Gerenciar vários contêineres, com tudo definido no arquivo `docker-compose.yml`. → [[Docker Compose]]

> [!question]- Para que servem os blocos version, network e volume?
> version: define as atualizações da sintaxe e os steps aceitos. network: cria uma rede para os serviços se comunicarem. volume: cria discos para os contêineres.

> [!question]- O que faz o depends_on?
> Faz a aplicação "x" iniciar só depois que a "y" estiver no ar.

> [!question]- Em `ports: 8002:3306`, como os outros contêineres e o acesso local chegam ao banco?
> Os outros contêineres pela 3306 (portaContainer). O acesso local pela 8002 (localhost:8002, portaDockerHost).

> [!question]- Quais são as políticas de restart?
> no (não reinicia), on-failure (reinicia em falha, saída diferente de zero), always (sempre que parar) e unless-stopped (sempre, exceto se for parado intencionalmente).

> [!question]- environment × env_file?
> environment é usado para setar as variáveis de ambiente e dar seus valores. env_file, usado no lugar dele, aponta para um arquivo `.env` do host.

> [!question]- O que acontece com o CMD ou ENTRYPOINT da imagem quando se usa command ou entrypoint no Compose?
> São substituídos pelos do Compose.

> [!question]- `docker compose stop` × `docker compose down`?
> stop paralisa os contêineres. down paralisa e remove os contêineres e seus componentes (rede, imagem, volume).

> [!question]- Qual comando aumenta o número de réplicas?
> `docker compose scale`.

> [!question]- No exemplo do Kong, para que servem links, build e o contexto?
> links: "linka" um contêiner com outro. build: "builda" a imagem do Dockerfile. O contexto define o local do Dockerfile (um ponto, se estiver na raiz).

## Aula 4 - Layers e ARG
> [!question]- O que é uma layer, e qual é a camada zero?
> Cada instrução do Dockerfile cria uma camada. O FROM é a camada zero. → [[Dockerfile e Camadas (Layers)]]

> [!question]- Se uma camada muda, o que acontece no próximo build?
> As camadas anteriores vêm do cache, e todas as seguintes são recriadas do zero.

> [!question]- Qual foi o ganho de tempo com o cache no exemplo?
> De cerca de 55 segundos para cerca de 15 segundos.

> [!question]- Em quais repositórios on-line o cache também se aplica?
> Docker Hub, AWS ECR, Azure Container Registry e Google Cloud Container Registry.

> [!question]- Para que usar ARG junto com ENV?
> Para não expor valores sensíveis no Dockerfile: o valor é passado no build.

## Aula 5 - Segurança
> [!question]- Qual ferramenta a aula usa para analisar vulnerabilidades?
> O Trivy, open source. → [[Trivy]]

> [!question]- Qual comando inicia o scan de uma imagem?
> `trivy image teste-trivy:latest` (a imagem é construída com a flag `-t`, que define a tag).

> [!question]- Quais são os níveis de severidade do Trivy?
> Unknown, Low, Medium, High e Critical.

> [!question]- Como mostrar só os níveis mais graves?
> `trivy image --severity CRITICAL,HIGH teste-trivy:latest`.

> [!question]- Qual vulnerabilidade da node:18 a aula mostra?
> O OpenSSH anterior à 9.3: o componente ssh-add adiciona chaves de Smartcard ao ssh-agent sem restrições (biblioteca openssl-client).

> [!question]- Como reduzir as vulnerabilidades de uma imagem?
> Usando imagens base mais enxutas, como a alpine. A imagem do Node 18 na variação alpine não teve nenhuma vulnerabilidade.

## Aula 6 - ECS
> [!question]- O que é o ECS?
> O serviço de gerenciamento de contêineres da AWS, que executa, escala e gerencia contêineres Docker num cluster de servidores. → [[ECS (Elastic Container Service)]]

> [!question]- O que é um cluster no ECS?
> Um conjunto lógico de instâncias EC2 ou de tarefas Fargate, onde os contêineres rodam.

> [!question]- Qual é a menor unidade de execução do ECS, e o que a define?
> A tarefa, definida por uma definição de tarefa (imagem Docker, CPU, memória, portas de rede e variáveis de ambiente).

> [!question]- O que faz um serviço no ECS?
> Mantém uma quantidade específica de tarefas rodando, reinicia as que falham e pode balancear a carga.

> [!question]- EC2 × Fargate?
> EC2 dá mais controle sobre as instâncias. Fargate é serverless, sem servidores para gerenciar.

> [!question]- Com quais serviços AWS o ECS se integra, e para quê?
> IAM (controle de acesso), CloudWatch (monitoramento) e ELB (balanceamento de carga). Também usa VPCs para isolar recursos.

> [!question]- Quais são os passos do fluxo de credenciais?
> 1) A instância busca suas credenciais no serviço de metadados do EC2. 2) O agente do ECS busca as credenciais de função. 3) O agente inicia a tarefa e define o segredo do contêiner. 4) A tarefa usa o segredo para buscar suas credenciais.

> [!question]- Cite os casos de uso do ECS.
> Desenvolvimento e teste, microsserviços, aplicações de alto desempenho, e Big Data e processamento em lote.

## Dúvidas em aberto
- [ ] **Promessas sem conteúdo no texto**:
  - aula 1: "principais comandos" e as diferenças VM × contêiner (só nas figuras);
  - aula 2: rede do contêiner, logs e registros de contêineres na cloud (ECR);
  - aula 3: o resumo repete rede, volume e logs;
  - aula 4: "problemas comuns e soluções" e "casos de uso avançado".
  Conferir nos vídeos.
- [ ] Os Dockerfiles e os `docker-compose.yml` dos exemplos estão em imagem nos PDFs.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
