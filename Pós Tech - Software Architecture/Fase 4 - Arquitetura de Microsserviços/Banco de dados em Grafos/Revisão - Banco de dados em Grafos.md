---
tags: [pos-tech/fase-4, grafos, revisao]
disciplina: Banco de dados em Grafos
---

# Revisão - Banco de dados em Grafos

[[Banco de dados em Grafos]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Fundamentos e Neo4j
> [!question]- Quem fundou a Teoria dos Grafos, e com qual problema?
> Euler, com o problema das sete pontes de Königsberg (1736): atravessá-las sem cruzar a mesma ponte duas vezes. → [[Labeled Property Graph]]

> [!question]- O que é o modelo LabeledPropertyGraph?
> Um grafo em que nós (entidades) e arestas (relações) podem ter rótulos, que os classificam, e propriedades, com informações adicionais.

> [!question]- Por que usar grafos em vez de relacional?
> Pela análise por contexto, em vez de por filtros; por ser a forma natural de pensar; e pela performance ao percorrer vários níveis, sem muitos joins ou queries recursivas.

> [!question]- Quando devo usar grafos?
> Com dados muito conectados e relações complexas (muitos joins), estruturas em árvore (como o BOM) e cenários em que o contexto importa (fraudes, comportamento de clientes).

> [!question]- Quais as três formas de começar a usar o Neo4j?
> AuraDB Free (nuvem; até 200 mil nós e 400 mil relacionamentos), Sandbox (nuvem, grátis) e Desktop (aplicação cliente). → [[Neo4j]]

> [!question]- Para que servem o Bloom e o Neodash, segundo a aula 1?
> Bloom: discovery para usuários de negócio sem conhecimento técnico profundo. Neodash: dashboards personalizados.

## Aula 2 - Modelagem
> [!question]- Como identificar nós, rótulos, relacionamentos e propriedades?
> Nós: substantivos. Rótulos: substantivos gerais. Relacionamentos: verbos. Propriedades: perguntas específicas. → [[Modelagem de Dados em Grafos]]

> [!question]- Duas pessoas chamadas João viram um nó só?
> Não: cada instância é um nó separado, com propriedades que as diferenciam.

> [!question]- Cite regras para migrar do relacional ao grafo.
> Tabela → rótulo, linha → nó, coluna → propriedade, só chaves de negócio, constraints e índices, FKs → relacionamentos, sem defaults, limpar duplicados, colunas indexadas → array, tabelas de junção → relacionamentos.

> [!question]- O que são nós intermediários, listas ligadas e árvores de linha do tempo?
> Nó intermediário: conexão com mais de duas entidades ou contexto (ex.: uma transação). Lista ligada: sequência ordenada com cabeça e cauda. Árvore de linha do tempo: eventos em níveis hierárquicos por intervalo de tempo (ex.: ano, mês, dia).

## Aula 3 - Cypher
> [!question]- O que caracteriza o Cypher?
> É declarativo (o "o que", não o "como"), usa notação de arte ASCII, encadeia as cláusulas e é a base do padrão ISO GQL. → [[GR 03 - Escrevendo consultas Cypher]]

> [!question]- O que significam `|`, `&` e `&!` nos rótulos?
> `|`: um rótulo ou outro. `&`: os dois ao mesmo tempo. `&!`: um rótulo, mas não o outro.

> [!question]- `()--()` × `()-->()` × `()<--()`?
> Sem direção; da esquerda para a direita; da direita para a esquerda.

> [!question]- Para que servem WITH, UNWIND e FOR EACH?
> WITH: agregados intermediários entre etapas. UNWIND: expandir uma lista em elementos. FOR EACH: modificar propriedades de cada elemento de uma lista.

> [!question]- O que faz `(a)-[*1..4]-(b)`?
> Busca conexões entre os dois nós a até quatro saltos (comprimento variável).

> [!question]- Como apagar nós com seus relacionamentos?
> Com `DETACH DELETE`.

## Aula 4 - Ingestão
> [!question]- Quais as opções de importação no Neo4j?
> LOAD CSV (Cypher), Neo4j Data Importer, PyIngest e outras (scripts, Spark, NiFi, Airflow). → [[Ingestão de Dados no Neo4j]]

> [!question]- O que preparar antes de importar?
> Rótulos, nomes de relacionamentos e propriedades, constraints e índices, e as consultas mais importantes.

> [!question]- Quais otimizações tornam o PyIngest eficiente?
> Blocos de tamanho configurável, Pandas para CSV e o parser de streaming ijson para JSON.

> [!question]- Em que ordem o PyIngest executa, e qual o cuidado com tipos?
> pre_ingest → files → post_ingest; todos os valores são lidos como strings, então é preciso converter no Cypher.

## Aula 5 - Visualização
> [!question]- Browser × Bloom × NeoDash?
> Browser: desenvolvedores, consultas ad-hoc em Cypher. Bloom: analistas, exploração no-code. NeoDash: especialistas de domínio e usuários de negócio, dashboards low-code. → [[Ferramentas de Visualização do Neo4j]]

> [!question]- Como funciona a busca no Bloom?
> Pela "Pesquisa de Grafos", com palavras-chave, como num mecanismo de busca, com drilldowns.

## Dúvidas em aberto
- Aula 1 × aula 5: o Bloom é para usuários de negócio (aula 1) ou para analistas de dados (aula 5)?
- Aula 4: o texto diz que o exemplo de LOAD CSV importa relacionamentos entre diretores e filmes, mas o código só cria os nós Movie.

## Pontos fracos (o que errei)
