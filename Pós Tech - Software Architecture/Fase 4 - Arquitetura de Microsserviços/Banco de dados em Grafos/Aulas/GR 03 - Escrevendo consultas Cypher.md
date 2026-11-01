---
tags: [pos-tech/fase-4, grafos, neo4j, cypher, aula]
disciplina: Banco de dados em Grafos
aula: 3
fonte: "Banco de dados em Grafos/10SOAT - Fase 4 - Banco de dados em grafos - Aula 03.pdf"
---

# GR 03 - Escrevendo consultas Cypher

← [[GR 02 - Modelagem de dados em grafos]] · [[Banco de dados em Grafos]] · Próxima → [[GR 04 - Ingestão de dados]]

> [!summary] Em uma frase
> O **[[Neo4j|Cypher]]** é uma linguagem de consulta **declarativa** para grafos: diz **"o que"** encontrar, não **"como"**. Os padrões parecem **arte ASCII**: `()` para nós e `-->` para relacionamentos. As cláusulas são **encadeadas**, e o Cypher é a **base do padrão ISO GQL**. A aula cobre **MATCH**, rótulos com `|`, `&` e `&!`, a direção dos relacionamentos, agregações, **WITH**, **UNWIND**, **FOR EACH**, funções de lista, estatísticas e de caminho, o **comprimento variável** e o **DETACH DELETE**.

## Hands On (vídeos)
Videoaulas com o Cypher no Neo4j, usando um **banco de dados de filmes**: **inserir, consultar e visualizar** dados.

**Para montar a base** (no Saiba Mais do PDF, "Escrevendo Consultas no Cypher"): criar um projeto no **Neo4j Sandbox** → abrir o **Neo4j Browser** pelo botão **Open** → digitar **`:guide hands-on`** e escolher a **base de filmes**.

## A linguagem
- **Declarativa** e própria para grafos: foca no **"o que"** deve ser encontrado. A notação dos padrões se assemelha a uma **arte ASCII**.
- **Estrutura encadeada**: cada cláusula passa seus resultados à próxima, o que facilita **filtrar, ordenar e limitar** em etapas.
- É a **base do padrão ISO GQL**.
- Segundo o resumo, a aula explorou **MATCH, CREATE e WHERE**.
- **MATCH** define o padrão a buscar; o **otimizador de consultas** escolhe a melhor forma de acessar os dados. **WHERE** e **CREATE** completam a consulta.
- **Figura 1 do PDF**: dois nós "Pessoa" ligados a um nó com os rótulos "Localizacao" **e** "Residencia".

## Padrões de nós
| Padrão | Significado |
|---|---|
| `()` | **Nó genérico**, sem rótulo nem propriedade |
| `(p:Pessoa)` | Nó com o rótulo **Pessoa**, referenciado pela **variável `p`**. Ex.: `MATCH (p:Pessoa) RETURN p` |
| `(:Localizacao)` | Nó com o rótulo, **sem variável**: útil para identificar nós de um tipo sem manipular suas propriedades; comum para verificar a existência de um nó com aquele rótulo |
| `(l:Localizacao)` / `(n:Residencia)` | Nó com rótulo e variável, para acessar propriedades e relacionamentos |
| `(x:Localizacao\|Residencia)` | Nó com o rótulo Localizacao **ou** Residencia |
| `(x:Localizacao&Residencia)` | Nó com **os dois** rótulos ao mesmo tempo |
| `(x:Localizacao&!Residencia)` | Nó com Localizacao **mas sem** Residencia (`&!` = exclusão) |

## Padrões de relacionamentos
| Padrão | Significado |
|---|---|
| `()--()` | Conexão **sem direção** especificada |
| `()-->()` | Da esquerda **para a direita** (ex.: rotas, hierarquias) |
| `()-[:CASADA_COM]->()` | Relacionamento de **tipo específico**, com direção |
| `()-[:MORA_EM\|DONA_DE]->()` | Um entre **vários tipos**, com direção |
| `()<--()` | Da direita **para a esquerda** |
| `()<-[]-()` | Qualquer tipo (`[]`), da direita para a esquerda: todas as conexões de entrada no nó da esquerda |

## Variáveis, retorno e filtros
- **Variáveis** representam nós e relacionamentos. O **RETURN** controla a saída: propriedades em **tabela** ou a representação **gráfica**.
- **Filtros** restringem os resultados (ex.: atores com papéis específicos).

## Agregação e iteração
| Recurso | O que faz |
|---|---|
| **sum(), avg(), min(), max(), count()** | Cálculos e sumarizações (ex.: total de vendas, média de idade) |
| **WITH** | Cria **agregados intermediários** e passa resultados de uma etapa para a próxima |
| **UNWIND** | Expande uma lista em elementos, como um **loop**. Ex.: `UNWIND [1,2,3] AS number RETURN number` |
| **FOR EACH** (assim no PDF) | Itera por uma lista e **modifica propriedades** de cada elemento, para alterações em massa (ex.: aumentar a idade de cada pessoa) |
| **RETURN** | Os resultados finais |

- **Funções de lista**: **collect()** (agrupa resultados numa lista) · **range()** (sequência numérica) · **isEmpty()** · **reverse()** · **head()** e **last()**.
- **Índices**: `List[0]` (primeiro) · `List[-1]` (último) · `List[1..5]` (do segundo ao quinto).
- **Funções estatísticas**: **percentileCont()** e **percentileDisc()** (percentis contínuos e discretos) · **stdev()** e **stdevp()** (desvio padrão).
- **Predicado e caminho**: **nodes(), labels(), relationships(), keys(), type(), properties()** acessam elementos; **all(), any(), none(), single()** verificam condições em listas; **exists()** verifica propriedades; **length()** mede caminhos.

## Comprimento variável
- `(a)-[*1..4]-(b)`: conexões entre dois nós a **até quatro saltos**. Essencial em redes complexas, como a **"teoria dos seis graus de separação"**.

## Limpando o banco
- **`DETACH DELETE`** exclui **nós e os relacionamentos associados**; útil com dados temporários em testes.

## Referências
Anthapu (2022) · Gupta (2015) · Revista Galileu (2023): seis graus de separação · Neo4j: Cypher Cheat Sheet · Robinson, Webber e Eifrem (2015)
