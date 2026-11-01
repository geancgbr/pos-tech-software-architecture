---
tags: [pos-tech/fase-3, api-gateway, kong, conceito]
aliases: [Konga, King, King for Kong]
---

# Konga e King

Interfaces gráficas **free** da comunidade para o [[Kong]], criadas antes de o Kong Manager ganhar versão free (3.4). Ambas se conectam ao **node do Kong Admin**.

| | Konga | King |
|---|---|---|
| Lado | **Server side**: configuração salva **globalmente** | **Client side**: configuração salva **localmente**; conecta ao node Admin a cada acesso |
| Login | **Sim** (o único com autenticação); começa pela criação do **usuário Master** | **Não** |
| Armazenamento | **Banco de dados** | Local |
| Destaques | Funcionalidades idênticas às do Kong Manager, mais **Users**, **Snapshots** e **Settings**; notificações por e-mail e Slack; permissões CRUD granulares | **Mapa de dependências baseado em Consumers** |
| Como sobe na aula | **Docker Compose** | Clone do repositório, **Dockerfile**, `docker build -t king .` e `docker run --publish 4200:80 -d king` (ou Docker Compose com Kong e banco) |

- **Veredito da aula 5**: o King, por ser client side e sem login, "acaba não sendo tão indicado"; o **Konga** é **superior** (mais funcionalidades e controle de acesso).
- O Konga ficou muito tempo **sem atualizações**, mas a comunidade está empenhada em atualizá-lo.

Aparece em: [[APIGW 04 - Conhecendo o Kong]], [[APIGW 05 - Criando serviços e rotas]]
