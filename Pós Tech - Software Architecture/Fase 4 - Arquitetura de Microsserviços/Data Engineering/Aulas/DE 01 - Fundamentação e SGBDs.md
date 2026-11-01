---
tags: [pos-tech/fase-4, banco-de-dados, aula]
disciplina: Data Engineering
aula: 1
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 01.pdf"
---

# DE 01 - Fundamentação e SGBDs

[[Data Engineering]] · Próxima → [[DE 02 - Bancos de documentos com MongoDB]]

> [!summary] Em uma frase
> Os bancos de dados são **componentes vitais** do software. Os **relacionais** (SGBDR/RDBMS, desde os anos 1970) organizam os dados em **tabelas** com **chaves primárias e estrangeiras** e usam **SQL**. Os **não relacionais** (**NoSQL**, "Not Only SQL", do fim dos anos 2000) surgiram para suprir limitações de **desempenho e escalabilidade** e se dividem em **documentos, colunares, chave-valor, grafos e séries temporais**. Ver [[Bancos Relacionais e Não Relacionais]].

## Hands On (vídeos)
As videoaulas aprofundam os conceitos e a diferença entre bancos **relacionais, documentais, colunares e de grafos**, mostrando em que uso cada modelo se adequa melhor.

## Relacional × não relacional
- Hoje a maioria das pessoas tem contato diário com bancos de dados (ex.: redes sociais): toda informação **persistente**, disponível de novo noutro dia ou dispositivo, está num banco.
- **Relacionais**: os mais **tradicionais** e populares, no mercado **desde os anos 1970**. Organizam os dados em **tabelas** (linhas = registros; colunas = atributos), com relações por **chaves primárias e estrangeiras**.
  - Também chamados **SGBDR** (Sistemas de Gerenciamento de Bancos de Dados Relacionais) ou **RDBMS**. Mais adotados: **MySQL, Oracle Database, Microsoft SQL Server, MariaDB e PostgreSQL** (Figura 1).
  - A grande maioria oferece **SQL** (Structured Query Language) para consulta, definição e manipulação.
- **Não relacionais**: qualquer banco que **não siga o modelo relacional**; também chamados **NoSQL (Not Only SQL)**.
  - A partir dos **anos 2000** surgiram alternativas que **não necessariamente** usam tabelas, linhas e colunas, para cenários com limitações de **desempenho e escalabilidade** no modelo relacional.
  - Os NoSQL surgiram **no final dos anos 2000**, quando o **custo do armazenamento caiu** drasticamente e cresceu a demanda por bases para quantidades altíssimas de dados.

> [!note] O texto diz que as alternativas surgiram "a partir dos anos 2000" e que os NoSQL surgiram "no final dos anos 2000". As aulas seguintes situam as origens de alguns tipos bem antes: chave-valor nos anos 1960 (aula 3), colunares nos anos 1970 (aula 4) e grafos nos anos 1960 (aula 5).

## Os tipos de bancos NoSQL
| Tipo | Características | Exemplos |
|---|---|---|
| **Documentos** (orientados a documentos) | Organização **sem esquema**: registros com atributos diferentes na mesma "tabela". Documentos geralmente em **JSON**. Normalmente têm linguagem de consulta e **podem ser facilmente escalados horizontalmente** | **MongoDB** ("constantemente classificado como o banco de dados NoSQL mais popular no mundo") |
| **Colunares** | Armazenam **em colunas**, não em linhas: recuperação mais eficiente em **consultas analíticas** (só as colunas relevantes são acessadas). Úteis para **grandes volumes** | **Apache Cassandra, HBase, Google Bigtable** |
| **Chave-valor** | Pares **chave → valor**; altamente escaláveis, **respostas rápidas** em escrita e leitura. Valores estruturados ou não. Usados para **caches, sessões de usuário e configuração** | **Redis, Riak, Amazon DynamoDB** |
| **Grafos** | Relacionamentos complexos: **nós** (entidades), **arestas** (relacionamentos) e **propriedades** (atributos). Ideais para **análise de rede, recomendações e detecção de padrões** | **Neo4j, Amazon Neptune, JanusGraph** |
| **Séries temporais** | Dados que **evoluem com o tempo** (sensores, eventos, métricas de desempenho), com consultas temporais | **InfluxDB, TimescaleDB, Prometheus** |

- Há também bancos **in-memory**, **espaciais** (dados geográficos), **de texto completo** (pesquisa textual) e outros (Figura 2).

## Diferenças principais
| Aspecto | Relacionais | Não relacionais |
|---|---|---|
| **Modelo de dados** | Tabelas com linhas e colunas; relações por chaves primárias e estrangeiras | Documentos, chave-valor, colunas, grafos: estruturação mais **flexível**, representando objetos e estruturas complexas diretamente |
| **Desempenho** | Otimizados para transações **ACID** (atomicidade, consistência, isolamento, durabilidade): transações seguras e **consistência rígida** | **Alta escalabilidade** e desempenho em leitura e gravação; geralmente priorizam **velocidade** e escala **horizontal** |
| **Esquema** | **Rígido e pré-definido** antes do armazenamento | **Flexível** ou até **ausente**: mais fácil e rápido adaptar o modelo |
| **Escalabilidade** | A **vertical** (mais recursos num único servidor) foi a abordagem **predominante** | Projetados para a **horizontal** (dados distribuídos em vários servidores) |

## Referências
Date (2004) · Elmasri e Navathe (2010) · Garcia-Molina, Ullman e Widom (2009) · Sadalage e Fowler, *NoSQL essencial* (2019) · Silberschatz (2020) · Tahaghoghi e Williams, *Learning MySQL* (2006)
