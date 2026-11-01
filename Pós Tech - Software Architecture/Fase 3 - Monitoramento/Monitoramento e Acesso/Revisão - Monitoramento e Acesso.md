---
tags: [pos-tech/fase-3, monitoramento, revisao]
disciplina: Monitoramento e Acesso
---

# Revisão - Monitoramento e Acesso

[[Monitoramento e Acesso]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução ao Zabbix
> [!question]- Por que o monitoramento é peça-chave, segundo a aula?
> Para desenvolver a aplicação de forma adequada: sem usar mais recursos do que se deve, sem estragar a performance e com insumos para melhorar a infraestrutura. → [[MON 01 - Introdução ao Zabbix]]

> [!question]- O que é o Zabbix?
> Um aliado open source que monitora praticamente tudo com pouca configuração e o Agent instalado, sem afetar a aplicação. → [[Zabbix]]

> [!question]- Por que o Docker precisa do WSL no Windows?
> Porque depende de um ambiente Linux e do Kernel, Cgroups e Namespaces para isolar os ambientes com containers.

> [!question]- Quais as peças do docker-compose.yml, e em que ordem?
> Rede (driver Bridge), MySQL (primeiro), Zabbix Server (`depends_on` no MySQL) e front-end (PHP com Apache, HTTP/HTTPS, `depends_on` no banco).

> [!question]- Por que usar variáveis e um arquivo .env?
> Para dados sensíveis: facilita na correção de problemas, além de não precisar procurar no YML onde os valores estão expostos.

> [!question]- Como subir e acessar o Zabbix?
> `docker compose up`, esperar o banco se configurar, abrir `http://localhost` e logar com Admin / zabbix.

## Aula 2 - Monitoramento com Zabbix
> [!question]- O que é o ODBC, segundo a aula?
> Uma ferramenta para se conectar ao banco de dados pelo Linux sem uma IDE gráfica. → [[ODBC]]

> [!question]- O que é preciso para monitorar um banco via ODBC?
> Um usuário e uma senha com permissão para analisar a tabela de performance do banco.

> [!question]- odbcinst.ini × odbc.ini?
> odbcinst.ini: os dados do conector e seu alias. odbc.ini: os dados do banco (endpoint, porta, usuário e senha); é único, e cada banco é separado pelo alias (ex.: `[db-zabbix]`).

> [!question]- Como testar a conexão antes de ir ao Zabbix?
> `isql -v db-zabbix`.

> [!question]- Por que o template certo é importante?
> Porque ele executa as querys que trazem as informações do banco (no caso, o template do MySQL).

> [!question]- Por que o host do banco não tem interface com IP?
> Porque a conexão é via ODBC, então não é preciso um Agent.

> [!question]- Quais macros precisam ser preenchidas?
> DSN (o nome da conexão usado no isql), User e Password. O Zabbix busca no odbc.ini e valida.

> [!question]- Por que os dados não apareceram no Latest Data, e como resolver?
> Por falta de permissão. Cria-se um usuário de monitoramento (`zbx_monitor`) com REPLICATION CLIENT, PROCESS, SHOW DATABASES e SHOW VIEW, e atualizam-se o odbc.ini e as macros.

## Aula 3 - Prometheus e Grafana (conteúdo: Loki e Promtail)
> [!question]- O que é o Grafana Loki, e como ele difere do Prometheus?
> Um projeto inspirado no Prometheus, mas com foco em logs; o Prometheus coleta métricas. → [[Grafana Loki]]

> [!question]- Por que o Loki precisa estar no mesmo servidor do Grafana?
> Segundo o PDF, porque é uma extensão da ferramenta.

> [!question]- Qual o papel do Promtail?
> Ler os logs com o comando `tail` do Linux e enviá-los ao Loki. → [[Promtail]]

> [!question]- Em que porta o Loki recebe os logs?
> 3100.

> [!question]- Quais as partes do config.yml do Promtail?
> positions (a posição de cada .log), clientes (a URL do Loki com a extensão de api), scrape (a varredura), labels (para as querys no Grafana e, com mais jobs, para isolar um conjunto de logs do outro) e path (onde estão os logs).

> [!question]- Como ver os logs no Grafana?
> Adicionar o Loki em Connections → Data sources (`http://localhost:3100`, Save & test), criar um painel com o Loki e filtrar pelos labels em Label Filters → Run Query.

## Dúvidas em aberto
- Aula 1: o texto diz que o MySQL deve estar "parecido com o da figura 1", mas a figura do MySQL é a 2.
- Aula 3: o PDF se chama "Prometheus e Grafana", mas trata de Loki e Promtail. O texto diz "já aprendemos sobre Zabbix, Grafana e Prometheus", sem aula de Prometheus nem de Grafana nos PDFs desta disciplina.
- Aula 3: o label aparece como `job: system` e como `job:varlogs`, e o arquivo do Promtail como `/etc/promtail/config.yml` e como `promtail.yml`.

## Pontos fracos (o que errei)
