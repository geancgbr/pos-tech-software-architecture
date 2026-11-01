---
tags: [pos-tech/fase-3, monitoramento, logs, aula]
disciplina: Monitoramento e Acesso
aula: 3
fonte: "Monitoramento e Acesso/Aula 03 - Prometheus e Grafana_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# MON 03 - Prometheus e Grafana

← [[MON 02 - Monitoramento com Zabbix]] · [[Monitoramento e Acesso]]

> [!summary] Em uma frase
> Nas três ferramentas já vistas (Zabbix, Grafana e Prometheus), **não vimos** uma seção de **logs**. O **[[Grafana Loki]]** é inspirado no Prometheus, mas **com foco em logs**: o **[[Promtail]]** lê os logs (com o `tail` do Linux) e os envia ao Loki (porta **3100**), e o **[[Grafana]]** os consulta por **labels**. Junto com o Zabbix e o Prometheus, **os logs** completam a stack de monitoramento.

> [!warning] Título × conteúdo
> O PDF se chama "Prometheus e Grafana", mas o conteúdo é a instalação do **Loki com Promtail** e a visualização dos logs no Grafana. O texto diz "já aprendemos sobre Zabbix, Grafana e Prometheus", mas os PDFs desta disciplina não trazem aula sobre Prometheus nem sobre Grafana.

## Hands On
Integrar logs com o **Grafana Loki** e o **Promtail** e analisá-los num **dashboard do Grafana**. Segundo o "O que vem por aí", tudo roda num projeto local, com o Loki instalado **via Ubuntu**.

## O Loki
- Projeto **inspirado no Prometheus**, mas **com foco em logs**, ao contrário do Prometheus, que **coleta métricas** de uma aplicação.
- Segundo o PDF, **precisa estar no mesmo servidor do Grafana**, porque é **uma extensão da ferramenta**.
- Assim como o Grafana, é **open source**.

## 1. Instalar
```bash
apt-get update
apt-get install loki promtail -y
```
O **Promtail** é responsável por **ler os logs usando o comando `tail`** do Linux (saída na Figura 1).

## 2. Configurar o Loki
Criar **`/etc/loki/loki.yml`** (Figura 2): a configuração que sobe o serviço Loki para que o Promtail o encontre e envie os logs pela **porta 3100**.

## 3. Configurar o Promtail
Um arquivo YML (Figura 3), salvo em **`/etc/promtail/config.yml`**:

| Parte | O que faz |
|---|---|
| **positions** (linha 5) | Aponta a **posição de cada arquivo `.log`** encontrado, "como um mapa para o Loki coletar" |
| **clientes** | A **URL do Loki** com a extensão de **api**, para o Promtail mandar os logs |
| **scrape** | O conjunto de configuração que faz a **varredura do sistema** |
| **labels** | Importantes para as **querys no Grafana** (ex.: `job: system`). Com mais jobs, os labels **isolam um conjunto de logs do outro** |
| **path** | Onde estão os logs a ler. Aqui, **todos os logs do Linux**, o que inclui Zabbix, Prometheus e processos do próprio Linux |

- **Permissão**: o usuário do Promtail precisa de **permissão de escrita** na pasta definida em positions:
  ```bash
  sudo chmod -R 700 /var/log
  ```
  > [!note] O texto não diz qual é a pasta de positions; o comando atua em `/var/log`.
- **Reiniciar** (primeiro o Promtail, depois o Loki):
  ```bash
  sudo systemctl restart promtail.service
  sudo systemctl restart loki.service
  ```

## 4. Ver os logs no Grafana
1. **Connections → Data sources** → adicionar o **Loki**. A única configuração é a URL **`http://localhost:3100`** (Figura 4). Depois, **Save & test**.
2. **Dashboards** → criar um painel com o **Loki como data source**.
3. Executar a query baseada nos **labels** definidos no Promtail (no arquivo da aula, **`job:varlogs`**; o nome é livre). Em **Label Filters**, adicionar os labels e clicar em **Run Query** (Figura 5).

> [!note] O texto cita o label como `job: system` ao explicar o arquivo e como `job:varlogs` no Grafana, e chama o arquivo de `/etc/promtail/config.yml` e depois de `promtail.yml`. Está assim no PDF.

## Conclusão do PDF
Junto com o **Zabbix** e o **Prometheus**, os logs **monitoram a infraestrutura e a aplicação** e **completam toda uma stack de monitoramento**. O mesmo processo poderia se aplicar a diversas outras aplicações e sistemas operacionais.

## Referências
Grafana Labs: Dashboards · Grafana Loki configuration parameters · Install locally
