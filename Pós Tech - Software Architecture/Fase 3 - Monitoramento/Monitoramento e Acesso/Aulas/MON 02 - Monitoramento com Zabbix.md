---
tags: [pos-tech/fase-3, monitoramento, zabbix, aula]
disciplina: Monitoramento e Acesso
aula: 2
fonte: "Monitoramento e Acesso/Aula 02 - Monitoramento com Zabbix_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# MON 02 - Monitoramento com Zabbix

← [[MON 01 - Introdução ao Zabbix]] · [[Monitoramento e Acesso]] · Próxima → [[MON 03 - Prometheus e Grafana]]

> [!summary] Em uma frase
> Além de servidores, o **[[Zabbix]]** monitora **bancos de dados via [[ODBC]]**: instala-se o **unixODBC**, configuram-se o **`odbcinst.ini`** (o conector) e o **`odbc.ini`** (os dados do banco), testa-se com **`isql`** e cria-se no Zabbix um **host** com o **template** do banco e as **macros** DSN, User e Password, **sem Agent**.

## Hands On
Instalar uma extensão **ODBC** para monitorar um banco de dados pelo Zabbix, fazer a conexão e monitorar via **hosts**.

## ODBC no Zabbix
- **ODBC**: segundo o PDF, uma ferramenta para **se conectar ao banco de dados pelo Linux** sem uma IDE gráfica.
- Dá para monitorar **diversos bancos**. Só são necessários **um usuário e uma senha com permissão** para analisar a **tabela de performance** do banco.
- A aula monitora o **banco do próprio Zabbix**, então não é preciso criar outro banco.

## 1. Instalar e configurar o unixODBC
```bash
sudo apt install -y unixodbc
ls /etc/odbcinst.ini              # se o arquivo existe, a instalação deu certo
```
- Pegar o caminho do **conector** (por padrão, `/usr/lib/x86_64-linux-gnu/odbc`, Figura 1).
- **`/etc/odbcinst.ini`** (`sudo nano /etc/odbcinst.ini`): o bloco de configuração do **conector**, aqui o do **MySQL**. O nome (em verde na Figura 2) é o **"alias"** do conector.
- **`/etc/odbc.ini`**: as informações do **banco**: **endpoint, porta, usuário e senha** (Figura 3).
- **Testar**: `isql -v db-zabbix`. Se os dados do `odbc.ini` estiverem corretos, o banco conecta (Figura 4). É só para garantir o funcionamento antes de criar o host.

| Arquivo | Guarda |
|---|---|
| `/etc/odbcinst.ini` | Os dados do **conector** e seu alias |
| `/etc/odbc.ini` | Os **dados do banco** (endpoint, porta, usuário, senha). É **único**, e o que separa uma configuração de banco da outra é o **alias** (ex.: `[db-zabbix]`) |

## 2. Criar o host no Zabbix
1. **Data Collection** → **Host** → **Create Host** (Figura 5).
2. Dar um **nome** e escolher o **template**. É importante escolher o **template correto**, porque ele executa as **querys** que trazem as informações do banco. Como o Zabbix da aula usa MySQL, o template tem de ser o do MySQL (Figura 6).
3. Pôr num **grupo**. **Não** se adiciona uma interface com IP ("assim como fizemos com servidores", diz o PDF, embora nenhuma aula da disciplina mostre isso): a conexão é via ODBC, então **não é preciso um Agent**.
4. Aba **Macros**: três macros vazias (Figura 7):

| Macro | O que é |
|---|---|
| **DSN** | O nome da conexão, o mesmo usado no `isql` |
| **User** | Usuário do banco |
| **Password** | Senha do banco |

Com essas três informações, o Zabbix busca no `odbc.ini` e valida a configuração.

5. **Add**: o host aparece na lista. Esperar a conexão e a coleta via ODBC.

## 3. Corrigir a permissão
Em **Monitoring → Latest Data**, os dados **não aparecem**, por **falta de permissão**. É preciso criar um **usuário específico para o monitoramento**:
```sql
-- logar com: sudo mysql -u root
CREATE USER 'zbx_monitor'@'%' IDENTIFIED BY 'zabbix';
GRANT REPLICATION CLIENT,PROCESS,SHOW DATABASES,SHOW VIEW ON *.* TO 'zbx_monitor'@'%';
```
- Atualizar o **`odbc.ini`** com o novo usuário e senha (Figura 9) e as **macros do host** (Figura 10).
- Esperar uns minutos e ver as métricas do banco em **Latest Data** (Figura 11).

## Referências
MySQL Product Archives · Unirede: O servidor Zabbix não está rodando: o que fazer? · Zabbix: MySQL by ODBC
