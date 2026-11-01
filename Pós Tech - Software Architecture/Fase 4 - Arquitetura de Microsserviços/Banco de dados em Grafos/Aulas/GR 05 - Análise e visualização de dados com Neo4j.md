---
tags: [pos-tech/fase-4, grafos, neo4j, aula]
disciplina: Banco de dados em Grafos
aula: 5
fonte: "Banco de dados em Grafos/10SOAT - Fase 4 - Banco de dados em grafos - Aula 05.pdf"
---

# GR 05 - Análise e visualização de dados com Neo4j

← [[GR 04 - Ingestão de dados]] · [[Banco de dados em Grafos]]

> [!summary] Em uma frase
> O Neo4j tem **três ferramentas principais** de análise e visualização: o **Neo4j Browser** (desenvolvedores, consultas **ad-hoc** em Cypher), o **Neo4j Bloom** (analistas, exploração **no-code**) e o **NeoDash** (usuários de negócio e especialistas de domínio, **dashboards low-code**). Ver [[Ferramentas de Visualização do Neo4j]].

## Hands On (vídeos)
Videoaulas conectando ao Neo4j e usando o **Browser**, o **Bloom** e o **NeoDash**: visualizações interativas, dashboards personalizados, filtros e consultas.

## Visão geral
| Ferramenta | Para quem (segundo o texto) | Destaques |
|---|---|---|
| **Neo4j Browser** | **Desenvolvedores** que dominam Cypher | Consultas **ad-hoc**, visualização de **pequenos grafos**, testes e estilização simples; **controle total** |
| **Neo4j Bloom** | **Analistas de dados** que conhecem o modelo, mas preferem o visual | Plataforma **no-code**, exploração visual avançada de **grandes grafos** |
| **NeoDash** | "**Especialistas de domínio**" e "**usuários de negócios**" | **Dashboards low-code** personalizáveis, relatórios visuais e insights |

- O PDF também traz uma tabela de "melhor ferramenta para cada perfil" (desenvolvedores que conhecem Cypher, analistas que conhecem o modelo de dados, usuários de negócio que precisam de uma visão refinada). Ver a tabela no PDF; a extração do texto não preserva as marcações de cada coluna.

## Neo4j Browser
- Ferramenta de **consulta e visualização** com interface gráfica: executa **Cypher** e mostra os resultados como **grafos, tabelas** ou estruturas de dados. "Especialmente útil para desenvolvedores e analistas".
- Suporta **CRUD**, com **autocompletar**, **alertas de sintaxe** e **documentação integrada**.
- **Personalização**: cores e tamanhos dos nós, organização em painéis. Ideal para **desenvolvimento e prototipagem**.
- Integra-se ao **Neo4j Workspace** e oferece funcionalidades para explorar dados importados, **testar algoritmos de grafos** e acompanhar consultas em tempo real (Figura 1).

## Neo4j Bloom
- Visualização **no-code**, sem precisar de Cypher, para **analistas de dados** e profissionais que querem uma visão clara e navegável.
- **"Pesquisa de Grafos"**: palavras-chave e termos, como num **mecanismo de busca**, com **drilldowns** nas conexões.
- **Personalização** de cores, formas e tamanhos; permite **salvar e compartilhar visões**.
- Parte do **Neo4j Workspace**; ajuda a **democratizar** o acesso a dados em grafos, de especialistas técnicos a gestores (Figura 2).

## NeoDash
- Ferramenta de **dashboard** para o Neo4j: **relatórios executivos** e dashboards personalizados, com **gráficos (e grafos)**, tabelas e componentes que vêm de **consultas Cypher**, numa interface **low-code**.
- **Layouts variados**, **widgets interativos** que reagem a entradas e filtros.
- **Consultas em tempo real** (dados sempre atualizados) e suporte a **múltiplas fontes de dados** (Figura 3).

> [!note] Perfis divergentes no PDF: o NeoDash é "indicado para especialistas de domínio" e, logo depois, "voltado para usuários de negócios"; o Browser é "voltado para desenvolvedores", mas "especialmente útil para desenvolvedores e analistas". Na aula 1, o **Bloom** é descrito como voltado para **usuários de negócios**; aqui, para **analistas de dados**. O Browser é para "visualização de pequenos grafos", mas a personalização dele ajuda "especialmente em grafos grandes e complexos", e o público dele ganha "cientistas de dados".

## Referências
Anthapu (2022) · Gupta (2015) · Neo4j: About Neo4j Bloom · Bloom Quick Start Guide · Neo4j Browser Manual · Neodash Developer Guide · Neodash User Guide · Robinson, Webber e Eifrem (2015)
