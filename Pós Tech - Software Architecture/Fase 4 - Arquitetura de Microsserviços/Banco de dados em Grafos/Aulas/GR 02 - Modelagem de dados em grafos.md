---
tags: [pos-tech/fase-4, grafos, neo4j, aula]
disciplina: Banco de dados em Grafos
aula: 2
fonte: "Banco de dados em Grafos/10SOAT - Fase 4 - Banco de dados em grafos - Aula 02.pdf"
---

# GR 02 - Modelagem de dados em grafos

← [[GR 01 - Fundamentos de grafos e a plataforma Neo4j]] · [[Banco de dados em Grafos]] · Próxima → [[GR 03 - Escrevendo consultas Cypher]]

> [!summary] Em uma frase
> Modelar em grafo é identificar, no domínio, os **substantivos** (nós), os **substantivos gerais** (rótulos), os **verbos** (relacionamentos) e as **perguntas** que geram **propriedades**. O PDF mostra como criar o modelo com **`MERGE`** em **[[Neo4j|Cypher]]**, como **migrar do relacional** (10 regras) e estruturas comuns: **nós intermediários, listas ligadas e árvores de linha do tempo**. Ver [[Modelagem de Dados em Grafos]].

## Hands On
Modelar os dados com as ferramentas da plataforma Neo4j.

## A modelagem
- Organiza as informações com foco nas **entidades (nós)** e suas **conexões (relacionamentos)**, em vez de tabelas. Ideal quando há **muitas relações complexas**: redes sociais, transações financeiras, redes de conhecimento.
- **Cenário hipotético**: **João e Maria moram em São Paulo** e são **amigos desde 2011**. Nós para João, Maria e São Paulo, ligados por relacionamentos.
- **Arrows** (arrows.app): ferramenta para desenhar o modelo; **círculos** são nós (com propriedades como nome e data) e **setas** são relacionamentos (também com propriedades, como a data de início de uma amizade) (Figura 1).

| Passo | Como identificar | Exemplo |
|---|---|---|
| **Descrever o domínio (nós)** | Os **substantivos** do contexto | "João", "Maria", "São Paulo"; em outros contextos, "cliente", "carro", "empresa" |
| **Rótulos (labels)** | **Substantivos mais gerais**, categorias ou grupos | "Pessoa", "Cliente", "Veículo". João e Maria poderiam receber "Pessoa" |
| **Relacionamentos** | Os **verbos** | "é amigo" e "mora em": "João é amigo de Maria", "João mora em São Paulo" (**direcionais**) |
| **Propriedades** | **Perguntas** específicas | "Quantos anos tem João?", "Desde quando João mora em São Paulo?" |

- **Cada instância é um nó**: várias pessoas chamadas João são **nós separados**, com propriedades únicas, o que evita duplicações e ambiguidades.
- Os **rótulos** são essenciais para **otimizar consultas**, porque selecionam rápido grupos de nós.
- Os **relacionamentos** podem ter propriedades ("desde", "data de início").
- As **propriedades** são **pares chave-valor** em nós ou relacionamentos.

## Gerando os dados no Neo4j (Cypher)
```cypher
MERGE (joao:Pessoa {nome: "João", idade: 50})
MERGE (maria:Pessoa {nome: "Maria", idade: 48})
MERGE (saoPaulo:Cidade {nomeCidade: "São Paulo"})
MERGE (joao)-[:MORA_EM {desde: 2022}]->(saoPaulo)
MERGE (maria)-[:MORA_EM {desde: 1998}]->(saoPaulo)
MERGE (joao)-[:É_AMIGO {desde: 2011}]->(maria)
```
- O **`MERGE`** cria nós com propriedades e relacionamentos **direcionais** com propriedades.

## Do relacional ao grafo (Tabela 1)
| Referência | Descrição |
|---|---|
| **Tabela → label** | Cada tabela de entidade vira um **rótulo** |
| **Linha → nó** | Cada linha vira um **nó** |
| **Coluna → propriedade do nó** | Os campos viram **propriedades** |
| **Só chaves primárias de negócio** | Remover as chaves **técnicas**, manter as **de negócio** |
| **Restrições e índices** | **Constraints exclusivas** para as chaves de negócio; **índices** para atributos de pesquisa frequente |
| **Chaves estrangeiras → relacionamentos** | Substituir as FKs por relacionamentos e **removê-las** depois |
| **Sem valores default** | Não armazenar valores padrão |
| **Limpar os dados** | Dados duplicados de tabelas desnormalizadas podem ir para **nós separados** |
| **Colunas indexadas → array** | `email1`, `email2`, `email3` podem indicar uma propriedade **array** |
| **Tabelas de relacionamento → relacionamentos** | Tabelas de junção viram relacionamentos; suas colunas viram **propriedades do relacionamento** |

- Ao trocar as FKs por relacionamentos, a navegação fica **mais direta**, sem a sobrecarga dos **joins** complexos.

## Dicas de modelagem
- Começar pelas **perguntas que o banco precisa responder**; priorizar as **consultas principais**; testar com **dados reais**.
- O Neo4j facilita a **refatoração** do grafo. Pensar **a longo prazo**, no crescimento dos dados.

## Estruturas comuns de grafo
| Estrutura | O que é | Exemplo do PDF |
|---|---|---|
| **Nós intermediários** | Representam uma conexão **mais complexa**, com mais de duas entidades ou com **contexto** no relacionamento; evitam relacionamentos diretos excessivos | Uma **transação** de venda ligando cliente, produto e data, com **valor** e **método de pagamento** |
| **Listas ligadas** | **Sequências ordenadas**, cada elemento ligado ao próximo; o primeiro é a **"cabeça"** e o último a **"cauda"**. Boas para consultas sobre o **item seguinte ou anterior** | **Episódios** de uma série, etapas de um processo |
| **Árvore de linha do tempo** | Eventos em ordem **cronológica**, com nós **hierárquicos** por intervalo de tempo; facilita consultas e agregações por período | Compras: nós de **ano** → **meses** → **dias**. Útil em registros históricos, transações e logs |
| **Múltiplas estruturas** | Mesclar as estruturas no mesmo grafo | — |

> [!note] As palavras-chave do PDF desta aula ficaram com o texto de modelo ("Palavra 1. Palavra 2. Palavra 3.").

## Referências
Anthapu (2022) · Gupta (2015) · Robinson, Webber e Eifrem (2015)
