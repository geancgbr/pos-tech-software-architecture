---
tags: [pos-tech/fase-3, monitoramento, zabbix, aula]
disciplina: Monitoramento e Acesso
aula: 1
fonte: "Monitoramento e Acesso/Aula 01 - Introdução ao Zabbix_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# MON 01 - Introdução ao Zabbix

[[Monitoramento e Acesso]] · Próxima → [[MON 02 - Monitoramento com Zabbix]]

> [!summary] Em uma frase
> O **[[Zabbix]]** é um aliado **open source** para monitorar "praticamente tudo" com pouca configuração e o **Agent** instalado, sem afetar a aplicação. Nesta aula, o **Zabbix Server** sobe junto do **MySQL** e do **front-end** com o **[[Docker Compose]]**.

## Hands On
Criar um **Zabbix Server com banco MySQL** a partir do **Docker Compose**, usando o arquivo YML.

## Por que monitorar
- O monitoramento é **peça-chave** para que o desenvolvimento de uma aplicação aconteça de forma adequada: **sem usar mais recursos do que se deve**, **sem estragar a performance** e com **insumos para aplicar melhorias** na infraestrutura.
- Isso é possível com um **monitoramento completo** e garantias de que tudo deve estar no devido lugar.
- **Zabbix**: aliado **open source** que monitora praticamente tudo com **pouca configuração** e o **Agent** instalado, o que **não afeta a aplicação**.
- Pode rodar numa **VM local**, numa **VM na nuvem** ou em **containers**. A aula usa o **Docker Compose**.

## Pré-requisitos
- **Docker** instalado com o **plugin do Docker Compose**.
- No Windows, pelo **WSL** (subsistema do Windows baseado em Linux), porque o Docker depende de um **ambiente Linux** e do **Kernel, Cgroups e Namespaces** para isolar os ambientes com containers ([[Cgroups e Namespaces]]).

## O docker-compose.yml, passo a passo
Criar o arquivo `docker-compose.yml` no VSCode, seguindo a **ordem do fluxo**:

| # | Peça | O que o PDF diz | Figura |
|---|---|---|---|
| 1 | **Rede** | Usada pelo Zabbix para se conectar ao banco. Driver **Bridge**, para garantir a conexão entre o host e o container e a internet para o Zabbix | Figura 1 |
| 2 | **MySQL** | Criado **primeiro**. Usar sempre **variáveis** para dados sensíveis e um arquivo **`.env`** com os valores, o que facilita na correção de problemas, **além de** não precisar procurar no YML onde os valores estão expostos | Figura 2 |
| 3 | **Zabbix Server** | Responsável por **se conectar ao banco**. Tem a flag **`depends_on`** apontando o MySQL, porque só pode ser criado depois do banco | Figura 3 |
| 4 | **Front-end do Zabbix** | Interface gráfica para acessar o Zabbix e **cadastrar os hosts**. Fica **virado para a internet**, com "os IPs de HTTP e HTTPS liberados e mapeados como portas" (assim no PDF). Roda em **PHP com Apache** e também tem `depends_on` apontando o banco | Figura 4 |

> [!note] O texto diz que o serviço MySQL "deve estar parecido com o da figura 1", mas a figura do MySQL é a 2 (a 1 é a rede).

## Subindo e acessando
```bash
docker compose up
```
- Aparecem os logs de cada aplicação. É preciso **esperar a configuração do banco**.
- Acessar **`http://localhost`** e logar com o usuário **Admin** e a senha **zabbix** (Figura 5).

## Referências
Docker Docs: Docker Desktop WSL 2 backend on Windows · Docker Hub: zabbix/zabbix-server-mysql · Microsoft: Como instalar o Linux no Windows com o WSL
