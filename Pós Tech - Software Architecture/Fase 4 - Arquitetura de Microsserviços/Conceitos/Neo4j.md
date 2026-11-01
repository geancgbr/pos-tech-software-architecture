---
tags: [pos-tech/fase-4, banco-de-dados, nosql, conceito]
aliases: [Cypher, Banco de grafos, Bancos orientados a grafos, Banco orientado a grafos]
---

# Neo4j

Banco **orientado a grafos** lançado em **2007**, da **Neo4j, Inc.**, com estrutura de **grafo nativa** ([[DE 05 - Bancos orientados a grafos com Neo4j]]).

- **Modelo**: **nós** (entidades, com propriedades) · **relacionamentos** (com **tipo**, direcionais ou bidirecionais; ex.: `AMIGO_DE`) · **propriedades** (em nós e relacionamentos).
- **Cypher**: linguagem **declarativa**, com sintaxe parecida com a notação de grafos.
- **Recursos**: escalabilidade horizontal, replicação, alta disponibilidade.
- **Edições**: Community (grátis, código aberto) · Enterprise (comercial) · **Aura** (DBaaS).

**Bancos de grafos em geral**: úteis quando os **relacionamentos importam tanto quanto os dados**; algoritmos como **DFS e BFS** (caminhos mais curtos, comunidades, centralidade); redes sociais, recomendações, bioinformática, **fraudes**. Exemplos: Neo4j, **Amazon Neptune**, JanusGraph.

## Na disciplina Banco de dados em Grafos
- **A plataforma** ([[GR 01 - Fundamentos de grafos e a plataforma Neo4j]]): fundada em **2007**, líder no mercado de bancos de grafos. Mais de **300 clientes corporativos**, **US$ 500 milhões** em investimentos, **170 parceiros**, **270 mil profissionais** e **100 milhões de downloads**. Mais de **65 algoritmos** (caminhos mais curtos, centralidade, comunidades, similaridade). Drivers para linguagens como Java, Python, JavaScript e .NET; conectores de ETL como **Kafka** e **Spark**.
- **Como começar**: **AuraDB Free** (nuvem; até 200 mil nós e 400 mil relacionamentos) · **Sandbox** (nuvem, grátis) · **Desktop** (aplicação cliente; ao criar o Local DBMS, seleciona-se a versão 5.x).
- **Modelo**: [[Labeled Property Graph]]; **modelagem** (com `MERGE`, [[GR 02 - Modelagem de dados em grafos]]): [[Modelagem de Dados em Grafos]].
- **Cypher** ([[GR 03 - Escrevendo consultas Cypher]]): declarativa, notação de **arte ASCII**, cláusulas encadeadas, **base do ISO GQL**. Padrões de nós (`(p:Pessoa)`, `|`, `&`, `&!`) e de relacionamentos (`--`, `-->`, `<--`, `[:CASADA_COM]`, `[:MORA_EM|DONA_DE]`), **MATCH, WHERE, CREATE, RETURN, WITH, UNWIND, FOR EACH**, funções de lista, estatísticas e de caminho, **comprimento variável** (`[*1..4]`) e **DETACH DELETE**.
- **Ingestão**: [[Ingestão de Dados no Neo4j]]. **Visualização**: [[Ferramentas de Visualização do Neo4j]].

Aparece em: [[DE 01 - Fundamentação e SGBDs]], [[DE 05 - Bancos orientados a grafos com Neo4j]], [[GR 01 - Fundamentos de grafos e a plataforma Neo4j]] a [[GR 05 - Análise e visualização de dados com Neo4j]]
