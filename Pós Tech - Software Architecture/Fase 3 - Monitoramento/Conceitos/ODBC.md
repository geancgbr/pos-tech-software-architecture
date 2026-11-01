---
tags: [pos-tech/fase-3, monitoramento, zabbix, conceito]
aliases: [unixODBC, odbc.ini, odbcinst.ini, isql]
---

# ODBC

Segundo a aula, o ODBC é uma ferramenta para **se conectar ao banco de dados pelo Linux sem uma IDE gráfica**. O [[Zabbix]] o usa para **monitorar bancos de dados**, com um usuário e uma senha que tenham permissão para analisar a **tabela de performance** do banco.

| Peça | Papel |
|---|---|
| **unixODBC** | O pacote instalado no Linux (`sudo apt install -y unixodbc`) |
| **`/etc/odbcinst.ini`** | O bloco de configuração do **conector**, com um **alias**. Caminho padrão do conector: `/usr/lib/x86_64-linux-gnu/odbc` |
| **`/etc/odbc.ini`** | Os dados do **banco**: endpoint, porta, usuário e senha. É **único**; cada banco é separado pelo **alias** (ex.: `[db-zabbix]`) |
| **`isql -v db-zabbix`** | Testa a conexão antes de criar o host no Zabbix |

- **No Zabbix**: host com o **template** do banco e as **macros DSN, User e Password**, que o Zabbix valida contra o `odbc.ini`. **Sem Agent** e sem interface com IP.
- **Permissão**: um usuário específico de monitoramento (`zbx_monitor`) com `REPLICATION CLIENT, PROCESS, SHOW DATABASES, SHOW VIEW`.

Aparece em: [[MON 02 - Monitoramento com Zabbix]]
