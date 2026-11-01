---
tags: [pos-tech/fase-4, grafos, neo4j, conceito]
aliases: [LabeledPropertyGraph, Grafo com Rótulos e Propriedades, LPG, Teoria dos Grafos]
---

# Labeled Property Graph

O modelo **LabeledPropertyGraph** (Grafo com Rótulos e Propriedades), usado em bancos de grafos como o [[Neo4j]] ([[GR 01 - Fundamentos de grafos e a plataforma Neo4j]]).

- **Nós** = entidades (pessoa, produto, local); **arestas** = relações ("amigo de", "comprou", "localizado em").
- Nós e arestas podem ter **rótulos** (classificação; ex.: "Usuário" e "Cliente") e **propriedades** (ex.: nome, idade, localização).
- Navega **diretamente** entre as relações, em vez de várias "ligações" dos bancos tradicionais: respostas rápidas mesmo em redes muito conectadas.
- **Usos**: redes sociais, sistemas financeiros (detecção de **fraudes**), gestão de dados de uma empresa.
- **Comparado ao relacional**: o modelo de pessoas e filmes fica **mais simples**, sem replicar `person_id` e `movie_id`.
- **Grafos em geral (performance)**: consultas por **vários níveis** (ex.: componentes de um carro) evitam muitos **joins** ou queries recursivas.

**Teoria dos Grafos**: o campo da matemática que estuda as **relações entre objetos**, fundado por **Euler** com o problema das **pontes de Königsberg** (1736). Um grafo tem **nós** e **arestas**.

Aparece em: [[GR 01 - Fundamentos de grafos e a plataforma Neo4j]]
