---
tags: [pos-tech/fase-4, grafos, neo4j, conceito]
aliases: [Modelagem em grafos, Nós intermediários, Listas ligadas, Árvore de linha do tempo]
---

# Modelagem de Dados em Grafos

Organizar as informações com foco nas **entidades (nós)** e nas **conexões (relacionamentos)** ([[GR 02 - Modelagem de dados em grafos]]).

| Elemento | Como identificar |
|---|---|
| **Nós** | Os **substantivos** do domínio (cada instância é um nó) |
| **Rótulos** | **Substantivos gerais** (categorias); otimizam as consultas |
| **Relacionamentos** | Os **verbos** (direcionais; podem ter propriedades) |
| **Propriedades** | **Perguntas** específicas; pares **chave-valor** |

**Do relacional ao grafo**: tabela → rótulo · linha → nó · coluna → propriedade · só chaves **de negócio** · **constraints** e **índices** · FKs → relacionamentos · sem valores default · limpar duplicados · colunas indexadas → **array** · tabelas de junção → relacionamentos.

**Dicas**: começar pelas **perguntas** que o banco precisa responder; priorizar as consultas principais; testar com dados reais; pensar no crescimento. O Neo4j facilita a **refatoração**.

**Estruturas comuns**: **nós intermediários** (ex.: uma transação ligando cliente, produto e data) · **listas ligadas** (sequências, com "cabeça" e "cauda") · **árvore de linha do tempo** (níveis hierárquicos por intervalo de tempo; ex.: ano → mês → dia) · múltiplas estruturas no mesmo grafo.

**Ferramenta**: o **Arrows** (arrows.app) para desenhar nós (círculos) e relacionamentos (setas).

Aparece em: [[GR 02 - Modelagem de dados em grafos]]
