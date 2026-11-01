---
tags: [pos-tech/fase-4, banco-de-dados, nosql, aula]
disciplina: Data Engineering
aula: 5
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 05.pdf"
---

# DE 05 - Bancos orientados a grafos com Neo4j

← [[DE 04 - Bancos colunares com Cassandra]] · [[Data Engineering]] · Próxima → [[DE 06 - Cloud e DBaaS]]

> [!summary] Em uma frase
> Os **bancos orientados a grafos** armazenam e consultam dados **altamente interconectados** como **nós** (vértices) e **arestas** (relacionamentos), com **propriedades**. São úteis quando **os relacionamentos importam tanto quanto os dados** (redes sociais, recomendações, fraudes). O **[[Neo4j]]** (2007) usa um grafo **nativo** e a linguagem **Cypher**.

## Hands On (vídeos)
**Primeiro vídeo**: as características dessa estrutura a partir de um cenário de exemplo, a **instalação** e os primeiros passos com o Neo4j. **Na sequência**: persistir os primeiros grafos (nós, relacionamentos e propriedades) e fazer consultas em **Cypher**.

> [!note] Esta aula chama a disciplina de "Database Engineering"; o nome do arquivo é "Data engineering".

## Grafos e bancos orientados a grafos
- **Grafo**: estrutura que representa **relacionamentos entre objetos**, com **nós** (vértices) e **arestas** que os conectam. Os nós podem ter **propriedades** (Figura 1).
- Usados para **redes sociais, recomendações, rotas de transporte, estruturas hierárquicas** e mais.
- No banco, cada **nó** é uma entidade e cada **aresta** uma relação; a representação facilita a **visualização** e as **consultas complexas** sobre relacionamentos (Figura 2, Star Wars).
- **Especialmente úteis** quando os relacionamentos são **tão importantes quanto os próprios dados**.
- **Algoritmos de percurso**, como **busca em profundidade (DFS)** e **busca em largura (BFS)**: descobrir padrões, **caminhos mais curtos**, **comunidades** e **métricas de centralidade**.
- **Áreas**: redes sociais, análise de redes, recomendação de produtos, **bioinformática**, **análise de fraudes**.
- **Exemplos**: **Neo4j, Amazon Neptune e JanusGraph**.
- **História** (segundo o PDF): surgiram nos **anos 1960**, com o desenvolvimento do modelo de dados em grafo por **Edgar F. Codd**, "pai dos bancos de dados relacionais", e ganharam popularidade nas últimas décadas. O **Neo4j** (2007) é um dos pioneiros.

| Vantagem | O que o PDF diz |
|---|---|
| **Modelagem flexível** | Entidades, relacionamentos e propriedades de forma **natural e intuitiva** |
| **Consultas eficientes** | Otimizados para **consultas de relacionamento**, mesmo em grandes conjuntos |
| **Dados altamente conectados** | Redes sociais, de transporte, de computadores: **influenciadores, comunidades, padrões** |
| **Escalabilidade horizontal** | Adicionar mais nós para aumentar armazenamento e processamento |
| **Integridade e consistência** | Regras de relacionamento e atualizações refletidas em todos os nós e arestas relacionados |

## O Neo4j
- Lançado em **2007**, desenvolvido pela **Neo4j, Inc.**, com estrutura de **grafo nativa** (nós, relacionamentos e propriedades).
- **Cypher**: linguagem **declarativa e intuitiva** para buscar, criar, atualizar e excluir nós e relacionamentos, com sintaxe que se assemelha à **notação de grafos**.
- **Escalabilidade horizontal** (mais servidores no cluster), **replicação** e **alta disponibilidade**.
- Segundo o PDF, "uma **solução comercial**, oferecendo diferentes edições", com uma comunidade ativa.

## Custos
| Edição | O que é |
|---|---|
| **Community Edition** | **Gratuita e de código aberto**, recursos básicos; projetos menores, desenvolvimento e testes |
| **Enterprise Edition** | Comercial completa: **alta disponibilidade, replicação, clusters, gerenciamento**; preço pela equipe de vendas |
| **Neo4j Aura** | **DBaaS** na nuvem; preço por tamanho, desempenho e armazenamento |

- Dependendo do projeto, **podem haver** custos adicionais de **hardware, armazenamento, manutenção e suporte**.

> [!note] O PDF chama o Neo4j de "solução comercial", mas também lista a Community Edition, gratuita e de código aberto.

## Modelagem de dados
| Elemento | O que é | Exemplo do PDF |
|---|---|---|
| **Nós (Nodes)** | Entidades ou objetos, com **propriedades** | Um **usuário** numa rede social, com nome, idade, localização |
| **Relacionamentos (Relationships)** | Conexões entre os nós; têm um **tipo** e podem ser **direcionais ou bidirecionais** | **`AMIGO_DE`** ligando dois usuários |
| **Propriedades (Properties)** | Atributos de nós **e** relacionamentos: strings, números, booleanos, datas | — |

- **Esquemas dinâmicos**: sem estrutura rígida antecipada.
- Considerar as **consultas e os padrões de acesso** ao modelar; boas práticas: identificar os **nós principais**, **tipos de relacionamento significativos** e **propriedades adequadas**.

## Referências
Documentação oficial do Neo4j · Neo4j Graph Academy · GraphAware · Paniz · Partner et al., *Neo4j in Action* · Robinson, Webber e Eifrem, *Graph Databases* · Sadalage e Fowler · Subramanya et al.
