---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 3
fonte: "Aula 03- Orquestração de Contêineres.pdf"
---

# DK 03 - Orquestração de contêineres

← [[DK 02 - Gerenciamento de contêineres]] · [[Dockerização]] · Próxima → [[DK 04 - Melhores práticas e solução de problemas]]

> [!summary] Em uma frase
> O [[Docker Compose]] gerencia **vários contêineres** a partir de um arquivo **`docker-compose.yml`**, que define serviços, redes e volumes. A aula detalha as instruções, as **políticas de restart** e os comandos do Compose.

## Hands On
O primeiro `docker-compose.yml`, escrito no VSCode e executado no terminal do WSL, criando os contêineres de forma automatizada e acessando-os pela Web. A aula também roda um **WordPress com banco MySQL**.

## O arquivo docker-compose.yml
Tudo é definido no arquivo. Também dá para criar um serviço apontando para um **Dockerfile**.

**Blocos principais**
- **version**: define as atualizações da sintaxe e os steps aceitos no arquivo.
- **network**: cria uma rede específica para os contêineres. Os serviços apontam para ela se precisarem se comunicar.
- **volume**: cria um disco para os contêineres. Pode haver mais de um, cada um com o nome seguido de dois pontos (`:`).

**Instruções dentro de `services`**
| Instrução | Para quê |
|---|---|
| **depends_on** | A aplicação "x" só inicia depois que a "y" estiver no ar |
| **image** | A imagem usada no serviço |
| **ports** | `portaDockerHost:portaContainer`. A **portaContainer** é a acessível **entre serviços**; a **portaDockerHost** é a usada **externamente**. Exemplo: com `8002:3306`, os outros contêineres conectam no banco pela **3306**, e o acesso local é por **localhost:8002** (Figura 1) |
| **restart** | A política de reinício (tabela abaixo). Cada serviço pode ter a sua |
| **environment** | Variáveis de ambiente (muitos serviços deixam variáveis vazias para serem preenchidas de fora). Alternativa: **env_file**, apontando para um arquivo `.env` do host |
| **volumes** | Apontam para um volume criado, ou para pastas específicas dentro dele |
| **command** e **entrypoint** | Alteram o start principal do contêiner, **substituindo o CMD ou ENTRYPOINT** da imagem ou do Dockerfile |

**Políticas de restart**
| Política | Comportamento |
|---|---|
| **no** | Não reinicia |
| **on-failure** | Reinicia em caso de **falha**, ou seja, quando a saída é **diferente de zero** |
| **always** | Reinicia **sempre** que parar de funcionar |
| **unless-stopped** | Reinicia sempre, **a menos que seja parado de forma intencional**. Serve para deixar um serviço "X" desligado |

## Comandos do Compose
| Comando | O que faz |
|---|---|
| `docker compose up` | Cria e inicia os contêineres |
| `docker compose build` | Só a etapa de build das imagens (facilita o "up") |
| `docker compose logs` | Mostra os logs |
| `docker compose restart` | Reinicia os contêineres |
| `docker compose ps` | Lista os contêineres |
| `docker compose scale` | Aumenta o número de réplicas de um contêiner |
| `docker compose start` | Inicia os contêineres |
| `docker compose stop` | Paralisa os contêineres |
| `docker compose down` | Paralisa e **remove** os contêineres e seus componentes (rede, imagem, volume) |

A diferença entre Docker e Docker Compose está na Figura 2 do PDF.

## Exemplo avançado: Kong API Gateway (Figura 3)
- **Serviços**: banco **Postgres** (a partir de um Dockerfile local), as **migrations** que atualizam as tabelas e o serviço **Kong**, que tem um API gateway com versão open source chamada **"Konga"**. Ela executa um comando que prepara o front-end criado pela comunidade, facilitando a criação de entradas no Kong API Gateway.
- **Usa**: arquivo `.env`, Dockerfiles e um arquivo `.sql` para criar um usuário no banco.
- Aparecem no exemplo:
  - **links**, uma instrução "não vista" até então, que "linka" um contêiner com outro;
  - a instrução **build**, que "builda" a imagem do Dockerfile;
  - o **contexto**, que define o local onde o Dockerfile estará (na raiz, usa-se um **ponto**).

## Referências
Docker Docs, *Compose Specification* · Baeldung, *Docker Compose Restart Policies* · 4Linux, *Dominando o Docker Compose*
