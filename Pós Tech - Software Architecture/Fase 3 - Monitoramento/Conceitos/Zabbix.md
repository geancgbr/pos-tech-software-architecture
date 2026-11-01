---
tags: [pos-tech/fase-3, monitoramento, zabbix, conceito]
aliases: [Zabbix Server, Zabbix Agent]
---

# Zabbix

## Na disciplina Monitoramento e Acesso (Fase 3)
Ferramenta **open source** de monitoramento que, segundo o PDF, monitora **"praticamente tudo"** com pouca configuração e o **Agent** instalado, sem afetar a aplicação. Pode rodar numa VM local, numa VM na nuvem ou em containers.

**Peças da instalação com Docker Compose** ([[MON 01 - Introdução ao Zabbix]])
| Serviço | Papel |
|---|---|
| **MySQL** | O banco do Zabbix, criado primeiro |
| **Zabbix Server** | Conecta-se ao banco (`depends_on` no MySQL) |
| **Front-end** | Interface gráfica em **PHP com Apache** para acessar o Zabbix e **cadastrar os hosts**, virada para a internet (HTTP e HTTPS) |

- Acesso em `http://localhost`, com o usuário **Admin** e a senha **zabbix**.
- **Hosts, templates e macros** ([[MON 02 - Monitoramento com Zabbix]]): o host é criado em **Data Collection → Host → Create Host**. O **template** executa as querys que trazem as informações; é preciso escolher o correto (na aula, como o Zabbix usa MySQL, o adequado ao MySQL). As **macros** guardam valores como **DSN, User e Password**. Via [[ODBC]], **não se adiciona interface com IP** ("assim como fizemos com servidores", diz o PDF) e **não é preciso Agent**.
- **Dados coletados**: em **Monitoring → Latest Data**.

## Na Fase 1
Na [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]], o Zabbix aparece como ferramenta que ajuda no monitoramento com **disparo de notificações**.

Aparece em: [[MON 01 - Introdução ao Zabbix]], [[MON 02 - Monitoramento com Zabbix]], [[MON 03 - Prometheus e Grafana]]
