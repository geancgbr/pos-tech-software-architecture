---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [docker-compose, docker-compose.yml, Compose, Políticas de restart]
---

# Docker Compose

Gerencia **vários contêineres**, com tudo definido no arquivo **`docker-compose.yml`**. Também cria serviços a partir de um **Dockerfile**.

**Blocos**: `version` (sintaxe e steps aceitos) · `network` (rede para os serviços se comunicarem) · `volume` (discos).

**Instruções de `services`**: `depends_on` · `image` · `ports` (`portaDockerHost:portaContainer`) · `restart` · `environment` ou `env_file` · `volumes` · `command` e `entrypoint`.

**No exemplo do Kong** também aparecem `links` ("linka" contêineres), a instrução `build` ("builda" a imagem do Dockerfile) e o contexto (o local do Dockerfile).

> [!tip] O exemplo de ports da aula
> Com `8002:3306`, os outros contêineres conectam no banco pela **3306**, e o acesso local é por **localhost:8002**.

**Políticas de restart**: `no` · `on-failure` (saída diferente de zero) · `always` · `unless-stopped` (só não reinicia se for parado intencionalmente).

**Comandos**: `up` · `build` · `logs` · `restart` · `ps` · `scale` (réplicas) · `start` · `stop` · `down` (para e remove os contêineres, a rede, a imagem e o volume).

Os exemplos da aula são **WordPress com MySQL** e **Kong API Gateway com Postgres e migrations**.

Detalhes: [[DK 03 - Orquestração de contêineres]]

## Na disciplina Monitoramento e Acesso (Fase 3)
Sobe o **[[Zabbix]] Server com MySQL e front-end**: rede com driver **Bridge**, variáveis para dados sensíveis, com os valores num arquivo **`.env`**, **`depends_on`** para criar o banco primeiro, e `docker compose up`. → [[MON 01 - Introdução ao Zabbix]]

Na disciplina API Gateway (Fase 3), o **Konga** sobe com Docker Compose, e o **King** também pode subir assim, num arquivo com o Kong e o banco ([[Konga e King]]).
