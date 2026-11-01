---
tags: [pos-tech/fase-4, banco-de-dados, nosql, aula]
disciplina: Data Engineering
aula: 4
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 04.pdf"
---

# DE 04 - Bancos colunares com Cassandra

← [[DE 03 - Bancos de chave-valor com Redis]] · [[Data Engineering]] · Próxima → [[DE 05 - Bancos orientados a grafos com Neo4j]]

> [!summary] Em uma frase
> Os **bancos colunares** armazenam os dados **em colunas**, não em linhas, o que os torna eficientes em **consultas analíticas e agregações** e dá **alta compressão**. O **[[Apache Cassandra]]** (criado no **Facebook**, doado à **Apache**) é distribuído, com arquitetura em **"ring"**, **famílias de colunas**, **CQL**, particionamento por **chave de partição** e **denormalização**.

## Hands On (vídeos)
**Primeiro vídeo**: os benefícios de uma base colunar, as diferenças de modelagem em relação ao relacional e a introdução e os primeiros passos com o Cassandra. **Segundo vídeo**: a arquitetura do Cassandra (resiliência a falhas, escalabilidade e replicação), a definição de **famílias de colunas** e a manipulação e consulta com **CQL**.

## Bancos colunares
- **SGBDs** que organizam os dados **em colunas**: os dados de cada coluna ficam **juntos**, numa estrutura otimizada.
- A **coluna** é a unidade de armazenamento e consulta; cada coluna tem valores de **um único tipo**, e as linhas são os conjuntos de valores correspondentes em todas as colunas.

| Vantagem | O que o PDF diz |
|---|---|
| **Consultas analíticas** | Só as colunas relevantes são acessadas: agregação, filtragem e **projeção seletiva** mais rápidas |
| **Alta compressão** | Pela **similaridade dos valores** numa coluna: economia de espaço |
| **Flexibilidade de colunas** | Adicionar e remover colunas **sem afetar** o desempenho ou os dados existentes |
| **Escalabilidade horizontal** | Dados distribuídos em vários nós |
| **Consultas complexas** | Filtros por colunas e projeções seletivas |

- **Exemplos**: **Apache Cassandra, Apache HBase e Amazon Redshift**, usados em **big data**, análise de dados, **séries temporais** e processamento em tempo real.
- **História** (segundo o PDF): surgiram nos **anos 1970**, com o desenvolvimento do banco relacional, e ganharam destaque com o **big data**. Uma implementação pioneira foi o **Vertica** (anos 2000), para consultas analíticas de alto desempenho. A evolução está ligada ao **processamento paralelo** e à **capacidade de armazenamento**.
- Ver a Figura 1 do PDF (exemplos de famílias de colunas).

## O Apache Cassandra
- Banco **distribuído de código aberto**, altamente **escalável e disponível**, desenvolvido pelo **Facebook** e doado à **Apache Software Foundation**.
- **Arquitetura descentralizada**, com replicação e particionamento em **"ring"**: dados distribuídos **uniformemente** entre os nós, **sem ponto único de falha**.

| Característica | O que o PDF diz |
|---|---|
| **Escalabilidade linear** | Mais nós = mais capacidade; distribuição **automática e transparente** |
| **Alta disponibilidade** | Replicação **síncrona e assíncrona** em vários nós |
| **Tolerância a falhas** | **Detecção** de falhas e **recuperação automática** |
| **Modelo flexível** | Baseado em colunas, com **esquemas dinâmicos** e alterações sem interrupção |
| **Consultas distribuídas** | Pela **CQL** (Cassandra Query Language), **semelhante ao SQL** |

- **Usos**: gerenciamento de conteúdo, **análise em tempo real**, **IoT** e aplicativos de **escala global**, com cargas intensas de leitura e gravação.

## Custos
**Gratuito** (licença **Apache 2.0**: usar, modificar e distribuir), mas, em produção, você **provavelmente precisará** de **hardware** para o cluster, e pode precisar de **recursos adicionais** (disco, balanceadores, gerenciamento) e **mão de obra qualificada** para configurar, monitorar e manter.

## Modelagem de dados
O Cassandra usa o modelo **"Wide Column Store"** ou **"Column Family Store"**.

| Característica | O que o PDF diz |
|---|---|
| **Famílias de colunas** | Também chamadas de **tabelas**; várias colunas identificadas pelo **nome**, sem esquema fixo |
| **Esquema flexível** | Adicionar ou remover colunas sem afetar os dados |
| **Particionamento e replicação** | Cada partição tem uma **chave de partição**, que determina **em qual nó** o dado fica |
| **Denormalização** | É comum **duplicar** informações em várias colunas ou famílias para evitar **junções** complexas |
| **Consultas por chave primária** | **Excepcionalmente rápidas**; consultas com vários filtros podem ser mais desafiadoras pela natureza distribuída |

> [!note] A aula diz que os colunares surgiram nos anos 1970, mas cita como implementação pioneira o Vertica, dos anos 2000. Também lista "suporte a consultas complexas" como vantagem dos colunares e diz que, no Cassandra, consultas complexas "podem ser mais desafiadoras".

- **Recomendação**: projetar o esquema **com base nas consultas** mais frequentes. Recursos avançados: **índices secundários** e **coleções**.
- Segundo o resumo, a aula também discutiu os mecanismos de **replicação e consistência** e boas práticas de consulta.

## Referências
Brown, *Learning Apache Cassandra* · Carpenter e Hewitt, *Cassandra: The Definitive Guide* · Documentação do Apache Cassandra · Lakshman e Prashant (2009) · Paniz · Sadalage e Fowler · Strickland
