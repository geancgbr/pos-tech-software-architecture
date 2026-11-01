---
tags: [pos-tech/fase-3, monitoramento, logs, conceito]
aliases: [promtail]
---

# Promtail

Responsável por **ler os logs usando o comando `tail`** do Linux e os **envia ao [[Grafana Loki|Loki]]**. Instalado junto com o Loki (`apt-get install loki promtail -y`) e configurado em **`/etc/promtail/config.yml`** (mais adiante, o PDF o chama de `promtail.yml`).

| Parte da configuração | Papel |
|---|---|
| **positions** | A posição de cada arquivo `.log`, "como um mapa para o Loki coletar" |
| **clientes** | A URL do Loki com a extensão de api |
| **scrape** | A varredura do sistema |
| **labels** | Usados nas querys do Grafana; isolam um conjunto de logs do outro quando há vários jobs |
| **path** | Onde estão os logs (na aula, todos os logs do Linux) |

- Precisa de **permissão de escrita** na pasta de positions (`sudo chmod -R 700 /var/log`) e é reiniciado com `sudo systemctl restart promtail.service`.

Aparece em: [[MON 03 - Prometheus e Grafana]]
