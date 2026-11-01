---
tags: [pos-tech/fase-4, grafos, neo4j, aula]
disciplina: Banco de dados em Grafos
aula: 1
fonte: "Banco de dados em Grafos/10SOAT - Fase 4 - Banco de dados em grafos - Aula 01.pdf"
---

# GR 01 - Fundamentos de grafos e a plataforma Neo4j

[[Banco de dados em Grafos]] · Próxima → [[GR 02 - Modelagem de dados em grafos]]

> [!summary] Em uma frase
> A **Teoria dos Grafos** nasceu com **Euler** e as **pontes de Königsberg** (1736). Um grafo tem **nós** e **arestas**; o modelo **[[Labeled Property Graph]]** (usado pelo Neo4j) acrescenta **rótulos** e **propriedades**. Grafos permitem análise **por contexto**, em vez de por filtros, e trazem um ganho de **velocidade** quando é preciso **percorrer vários níveis**. A **[[Neo4j]]** (2007) é líder no mercado de bancos de grafos e pode ser usada pelo **AuraDB Free**, pelo **Sandbox** ou pelo **Desktop**.

## Hands On (vídeo)
Usar o Neo4j em três ferramentas: **Neo4j AuraDB Free**, **Neo4j Desktop** e **Neo4j Sandbox**, com a videoaula guiando cada passo. Segundo o resumo, também se criaram **grafos simples** no Neo4j.

## Teoria dos Grafos
- **Leonard Euler** (assim no texto; nas referências, "Leonhard"): matemático do **século XVIII**, nascido em **15 de abril de 1707**, em **Basileia** (Suíça), com passagens pelas academias de **São Petersburgo** e de **Berlim**.
- É reconhecido como **fundador da Teoria dos Grafos**, pelo problema das **sete pontes de Königsberg** (**1736**): era possível atravessá-las **sem cruzar a mesma ponte duas vezes**? Ao resolver, criou a base do campo (Figuras 1 a 4).
- **Teoria dos Grafos**: estuda as **relações entre objetos**. Usos: redes sociais, **rotas de entrega**, interação entre **proteínas** numa célula.
- Um grafo tem **nós** (os objetos) e **arestas** (as conexões).
- Em bancos como o Neo4j, as relações são consultadas de forma **extremamente eficiente**, comparado aos relacionais, que **não são otimizados para consultas complexas de relacionamento**.

## Labeled Property Graph
Ver [[Labeled Property Graph]].
- **Nós** = entidades (pessoa, produto, local); **arestas** = relações ("amigo de", "comprou", "localizado em").
- Nós e arestas podem ter **rótulos** (que os classificam) e **propriedades** (informações adicionais). Ex.: uma pessoa com os rótulos **"Usuário"** e **"Cliente"** e as propriedades **nome, idade, localização**.
- **Usos**: redes sociais (amigos, interesses, interações) e sistemas **financeiros** (contas, pagamentos, datas, valores), útil para detectar padrões e identificar possíveis **fraudes**.
- Em vez de várias **"ligações"** como nos bancos tradicionais, os grafos **navegam diretamente** entre as relações, com respostas rápidas mesmo em redes muito conectadas.

## Por que grafos em vez de relacional
| Motivo | O que o PDF diz |
|---|---|
| **Análise por contexto, não por filtros** | Filtrando "pessoas inovadoras" com mentes excêntricas, que contestaram paradigmas, fascinadas por ciência e extravagantes, aparecem **Salvador Dalí** e **Nikola Tesla**, de contextos muito diferentes (arte surrealista × engenharia elétrica). Uma análise em grafo, olhando **contexto, trabalhos e conexões**, daria outra visão |
| **A forma natural de pensar** | Para pessoas e filmes no relacional, podemos pensar em criar entidades **Person**, **Movie** e várias entidades de relação (Figura 5); no grafo, o modelo fica **mais simples**, sem replicar `person_id` e `movie_id`, porque os relacionamentos já indicam a conexão (Figura 6) |
| **Performance** | Recuperar dados **passando por vários níveis**. Ex.: os **componentes de um carro**, cada um composto por outros, em infinitos níveis (porta → motor de vidro elétrico → engrenagem...). No relacional, uma FK `componente_pai_id` exige **muitos joins** ou uma **query recursiva**, com performance "muito comprometida"; no grafo, a estrutura já está **armazenada de forma conectada** (Figura 7) |

- Com **poucos níveis**, a diferença pode ser mínima; segundo o PDF, quanto mais conectada a base, "maior será o impacto na performance caso você utilize uma base de dados em grafo".

## Quando usar grafos
- Dados com **muitas conexões** e relações complexas, em que consultas com **múltiplos joins** ficam lentas (produtos e fornecedores, interações em redes sociais).
- **Estruturas em árvore**, como as **listas de materiais (BOM, Bill of Materials)** em cadeias de suprimentos, com rastreamento por vários níveis.
- **Mudanças frequentes** nos dados e cenários em que o **contexto importa** (comportamento de clientes, **padrões de fraude**): prever ações, como clientes com potencial de compra ou **anomalias** em transações.

## A plataforma Neo4j
- Fundada em **2007**; a ideia surgiu de desenvolvedores com dificuldade em sistemas relacionais ao trabalhar com dados **altamente conectados**. Hoje é **líder** no mercado de bancos de grafos.
- **Números**: mais de **300 clientes corporativos** (muitos com faturamento acima de **US$ 1 bilhão**) · mais de **US$ 500 milhões** em investimentos · mais de **170 parceiros** · mais de **270 mil profissionais** · mais de **100 milhões de downloads**.
- **Algoritmos**: mais de **65** prontos: **caminhos mais curtos** (rotas), **centralidade** (influenciadores), **detecção de comunidades** e **similaridade** (recomendações). Ver a Figura 8 (componentes da plataforma).
- **Integração**: drivers para linguagens como **Java, Python, JavaScript e .NET**, e conectores de **ETL** como **Apache Kafka** e **Spark**.
- **Visualização**: **Bloom** (discovery intuitiva para usuários de negócio, sem conhecimento técnico profundo) e **Neodash** (dashboards personalizados com métricas, gráficos e mapas).

## Como começar
| Opção | O que é | Passos |
|---|---|---|
| **Neo4j AuraDB Free** | Plataforma de grafos **em nuvem**, rápida, escalável, automatizada. Limite de **200 mil nós e 400 mil relacionamentos** | console.neo4j.io → "Create Instance" → **"AuraDB Free"** → nome → **guardar a senha gerada** → esperar 3 a 5 minutos |
| **Neo4j Sandbox** | Instância **gratuita em nuvem** para aprender, testar ideias ou explorar dados pré-construídos | sandbox.neo4j.com → login → "New Project" → **"BlankSandbox"** |
| **Neo4j Desktop** | **Aplicação cliente** para iniciantes e experientes | Baixar → criar um projeto → "Add" → **"Local DBMS"** → nome e senha (**mínimo de 8 caracteres**) → versão **5.x** → "Criar" |

## Referências
Anthapu, *Graph Data Processing with Cypher* (2022) · Gupta, *Neo4j Essentials* (2015) · Lazarevic e Lyon (2021) · Robinson, Webber e Eifrem, *Graph Databases* (2015) · Wikipedia
