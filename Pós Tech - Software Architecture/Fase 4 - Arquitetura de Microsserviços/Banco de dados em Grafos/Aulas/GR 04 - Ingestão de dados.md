---
tags: [pos-tech/fase-4, grafos, neo4j, aula]
disciplina: Banco de dados em Grafos
aula: 4
fonte: "Banco de dados em Grafos/10SOAT - Fase 4 - Banco de dados em grafos - Aula 04.pdf"
---

# GR 04 - Ingestão de dados

← [[GR 03 - Escrevendo consultas Cypher]] · [[Banco de dados em Grafos]] · Próxima → [[GR 05 - Análise e visualização de dados com Neo4j]]

> [!summary] Em uma frase
> Há várias formas de **importar dados no [[Neo4j]]**: o **`LOAD CSV`** do Cypher (CSV local, por URL ou em buckets), o **Neo4j Data Importer** (interface gráfica, sem código, para CSV e JSON) e o **PyIngest** (script Python para grandes volumes), além de scripts próprios, **Spark** e plataformas de ETL (**NiFi**, **Airflow**). Antes, é preciso **preparar** rótulos, relacionamentos, propriedades, **constraints** e **índices**. Ver [[Ingestão de Dados no Neo4j]].

## Hands On (vídeos)
Videoaulas importando dados no Neo4j com **LOAD CSV**, **Neo4j Importer** e **PyIngest**, em cenários reais em que um CSV é **carregado, transformado e conectado** no grafo.

## As opções (Figura 1)
| Opção | O que o PDF diz |
|---|---|
| **Cypher `LOAD CSV`** | Carrega CSV **local, por URL ou em buckets na nuvem**, como um **fluxo** de registros, linha a linha; permite **transações**, **transformar e converter** valores. "Ideal para arquivos estruturados", com controle preciso de cada registro |
| **Neo4j (Data) Importer** | Ferramenta para **CSV e JSON**, com **interface gráfica**, sem código, para **testes e protótipos** |
| **PyIngest** | Script em **Python** com **maior controle e desempenho** para **grandes volumes** |

- O Importer e o PyIngest suportam CSV e JSON e podem ser usados no **Neo4j Desktop** e no **Sandbox**.
- A Figura 1 compara as formas pela **velocidade** e pelo **esforço de implementação**.

## Preparação
- Definir os **rótulos**, os **nomes dos relacionamentos** e das **propriedades**.
- Criar as **restrições (constraints)** e os **índices** necessários.
- Definir as **consultas mais importantes**, para evitar retrabalho.

**Passos com o Cypher**: definir a estrutura do CSV e garantir **IDs únicos** → verificar se os dados estão **"limpos"** → criar **restrições** → executar o Cypher de carga → adicionar **índices** para as consultas futuras.

## Exemplo com LOAD CSV
Cria nós **Movie** com título, voto médio, ano e gêneros; o PDF diz que os relacionamentos também são importados, ligando **diretores e filmes**.
```cypher
:auto
LOAD CSV WITH HEADERS FROM
'https://data.neo4j.com/v4.0-intro-neo4j/movies1.csv' AS row
CALL {
  WITH row
  MERGE (m:Movie {id:toInteger(row.movieId)})
  ON CREATE SET
    m.title = row.title,
    m.avgVote = toFloat(row.avgVote),
    m.releaseYear = toInteger(row.releaseYear),
    m.genres = split(row.genres,":")
} IN TRANSACTIONS OF 100 ROWS
```
> [!note] O código do PDF cria só os nós Movie; a parte dos relacionamentos entre diretores e filmes, citada no texto, não aparece no trecho. A indentação foi refeita.

## Neo4j Data Importer
- Agiliza **testes e protótipos** **sem código**, carregando **flat files** pela interface gráfica, **sem acesso ao sistema de arquivos** do banco.
- **Não cobre todas as necessidades**; alternativas: **LOAD CSV**, **PyIngest** e plataformas de ETL como **Apache NiFi** e **Spark**.
- Disponível no **Neo4j Workspace** (instâncias **AuraDB**, aba **"Import"**, com consultas e exploração visual) e numa **versão independente**: `https://data-importer.neo4j.io/` (segura) ou `https://data-importer.graphapp.io/` (não segura, para restrições de navegador). **Recomendação**: usar a conexão **segura** (Figura 2).

## PyIngest
Script em **Python 3** que carrega **CSV e JSON** no Neo4j, com otimizações:
- registros agrupados em **blocos de tamanho configurável**;
- **CSV** com a biblioteca **Pandas**;
- **JSON** com o parser de streaming **ijson**, sem carregar o documento inteiro na memória.

**Instalação e uso**
```bash
pip3 install -r requirements.txt
pip3 install pyyaml          # se o módulo yaml faltar
python3 ingest.py <config>   # <config> = arquivo YAML com os parâmetros
```
- **Sequência**: comandos **`pre_ingest`** → as importações da seção **`files`** → comandos **`post_ingest`**.
- **Atenção**: **todos os valores são lidos como strings**; converta no Cypher se precisar de outro tipo.

| Configuração | O que é |
|---|---|
| `server_uri` | Endereço do driver Neo4j (**obrigatório**) |
| `admin_user` / `admin_pass` | Usuário e senha (**obrigatórios**) |
| `pre_ingest` / `post_ingest` | Comandos Cypher antes e depois da importação |
| `files` | Cada arquivo: `url`, `cql`, `chunk_size`, `type` (csv ou json) |

| Parâmetro de arquivo | O que é |
|---|---|
| `url` | Caminho do arquivo (**obrigatório**) |
| `cql` | Comando Cypher (**obrigatório**) |
| `chunk_size` | Registros por lote (**padrão: 1000**) |
| `field_separator` | Só CSV; separador (**padrão: vírgula**) |
| `compression` | `gzip`, `zip` ou `none` |
| `skip_file` / `skip_records` | Ignorar o arquivo ou pular registros iniciais |

> [!note] O Spark aparece ora entre as "plataformas de ETL" (com o NiFi), ora como "ferramenta de processamento de dados", com as plataformas de ETL sendo NiFi e Airflow. Na aula 1, Kafka e Spark são "ferramentas de ETL".

## Outras formas
Scripts em **Python, Java e NodeJS**, o **Spark** e plataformas de ETL como **Apache NiFi** e **Apache Airflow**, para fluxos de dados complexos.

## Referências
Anthapu (2022) · Gupta (2015) · Neo4j: Overview of Importing Data into Neo4j · Robinson, Webber e Eifrem (2015)
