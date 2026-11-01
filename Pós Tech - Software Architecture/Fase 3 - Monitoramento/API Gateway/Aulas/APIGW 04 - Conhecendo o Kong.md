---
tags: [pos-tech/fase-3, api-gateway, kong, aula]
disciplina: API Gateway
aula: 4
fonte: "API Gateway/POSTECH - Aula4_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# APIGW 04 - Conhecendo o Kong

← [[APIGW 03 - API Management na prática]] · [[API Gateway]] · Próxima → [[APIGW 05 - Criando serviços e rotas]]

> [!summary] Em uma frase
> O **[[Kong]]** é um **API Gateway open source** que serve como **proxy para APIs**, com configurações de **autenticação, logs e consumers**. Para administrá-lo graficamente há o **Kong Manager** (com versão free desde a **3.4**) e as opções da comunidade, **Konga** e **King** ([[Konga e King]]). Esta aula é sobre o **Konga**.

## Hands On (vídeo)
Conhecer o **Konga** e ver as diferenças em relação ao **Kong Manager**. Segundo o PDF, na videoaula o Konga foi **instalado, mas não usado**, e o documento da aula explica como usá-lo. Ele subiu com o **[[Docker Compose]]** (link nas referências do PDF).

## Kong Manager, Konga e King
- O **Kong Manager** era **pago**; desde a **versão 3.4**, há uma versão **free**, mais **básica** e **sem autenticação** para acessar serviços, rotas e consumers, mas com o **core** de funcionalidades para criar e manter serviços e rotas.
- Antes da 3.4, a comunidade criou opções **free**: as mais conhecidas são o **Konga** e o **King**, **interfaces gráficas** que se conectam ao **node do Kong Admin** e obtêm as informações do gateway.

| | King | Konga |
|---|---|---|
| Lado | **Client side**: a configuração fica **salva localmente**, e a cada acesso ele se conecta ao node Admin | **Server side**: a configuração fica salva **globalmente**, não na sessão |
| Login | **Não tem** tela de login | **O único** com tela de **autenticação** |
| Armazenamento | Local | **Banco de dados** |

## Usando o Konga
1. **Primeiro acesso**: a tela de criação do **usuário Master** (Figura 1). Depois, login com o usuário e a senha definidos.
2. **Conexão com o node do Kong Admin**: pelo docker compose, a porta é a **8001**. Conforme a URL é exposta, funciona com **`localhost`** ou com o endpoint interno do Docker, **`host.docker.internal`** (Figura 2).
   - A conexão pode ser **só pela URL e porta** ou por **Key, JWT ou Basic auth**, usando as informações de um **Consumer** (pode-se criar um exclusivo). Por padrão, a aula conecta **só pela URL**.
3. **Tela inicial** com informações importantes; em **"Info"**, detalhes do sistema (Figura 3).

> [!note] O Saiba Mais diz que as funcionalidades do Konga são "idênticas" às do Kong Manager (com três campos exclusivos); o resumo da aula diz que elas "são diferentes".

**As funcionalidades são idênticas às do Kong Manager**, com **três campos exclusivos**:
| Campo | O que faz |
|---|---|
| **Users** | Cria usuários **comuns e admins** do Konga |
| **Snapshots** | Um **snapshot** de tudo no node ativo: **Serviços, Rotas, APIs, Plugins, Consumers, Upstreams e Targets** |
| **Settings** | Configurações do Konga, como **liberar ou não** o cadastro de usuários (se negado, um administrador cria) |

- Também envia **notificações** por **e-mail e Slack**, e as permissões de novos usuários são **granulares** (**create, read, update e delete**). Por padrão, o **Admin** tem todas (Figura 4).
- A **URL do Konga** pode ser personalizada, e a configuração é feita **pelo node do Kong**.
- O Konga ficou **muito tempo sem atualizações**, mas a comunidade está empenhada em atualizá-lo.

## Referências
dougls/Kong-Konga-DockerCompose (GitHub) · Kong Docs: Kong Gateway · Konga: Kong GUI
