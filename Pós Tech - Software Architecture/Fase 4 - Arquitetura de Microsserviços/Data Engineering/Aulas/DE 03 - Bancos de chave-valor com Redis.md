---
tags: [pos-tech/fase-4, banco-de-dados, nosql, aula]
disciplina: Data Engineering
aula: 3
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 03.pdf"
---

# DE 03 - Bancos de chave-valor com Redis

← [[DE 02 - Bancos de documentos com MongoDB]] · [[Data Engineering]] · Próxima → [[DE 04 - Bancos colunares com Cassandra]]

> [!summary] Em uma frase
> Os **bancos de chave-valor** guardam pares **chave única → valor**, com **acesso muito rápido por chave**. Por isso são usados em **cache, sessões** e qualquer cenário de **lookup rápido**. O **[[Redis]]** ("Remote Dictionary Server") é de código aberto, com vários tipos de dados (strings, listas, conjuntos, sorted sets, hashes), **pub/sub**, scripts **Lua**, persistência, **expiração de chaves**, clusters e replicação.

## Hands On (vídeos)
As características dos bancos de chave-valor e a **instalação** e os primeiros passos com o Redis local. Depois, a prática: as diferenças entre **bases de dados e namespaces** no Redis e os comandos para **manipular e consultar** chaves e valores. Segundo o resumo, também se viram as boas práticas com **TTL**, armazenamento permanente e configurações básicas.

## Bancos de chave-valor
- Tipo de NoSQL que armazena **pares de chave e valor**: cada registro tem uma **chave única** associada a um valor.

| Característica | O que o PDF diz |
|---|---|
| **Simplicidade** | Modelo simples, fácil até para devs inexperientes |
| **Alta velocidade** | Otimizados para acesso por chave, com **índices eficientes** e **baixa latência** |
| **Escalabilidade horizontal** | Fácil adicionar servidores |
| **Flexibilidade** | Valores de **qualquer tipo**, de strings a **JSON** |
| **Tolerância a falhas** | Muitos são **distribuídos**, com replicação integrada |
| **Baixa complexidade de consulta** | Ótimos por chave, mas **podem ter limitações** em consultas complexas com relacionamentos |

- **Usos**: **cache**, **sessões**, **metadados**, **sistemas de recomendação** e outros casos em que o acesso por chave é prioritário.
- **Exemplos**: **Redis, Amazon DynamoDB e Riak**. Segundo o PDF, as principais opções no mercado hoje são o **Redis** e o **Amazon DynamoDB**.
- **História**: os primeiros sistemas são dos **anos 1960**, como o **IMS** (Information Management System) da **IBM**, de **1966**, com modelo hierárquico e estrutura de chave-valor. O conceito moderno veio com a **Web**; o pioneiro foi o **Dynamo**, da **Amazon**, em **2004**, para o comércio eletrônico.

## O Redis
| Recurso | O que o PDF diz |
|---|---|
| **Velocidade** | **Milhões de operações por segundo** |
| **Modelo versátil** | Strings, listas, conjuntos, hashes e **sorted sets** |
| **Recursos avançados** | **Pub/sub** (canais de mensagens) e **scripts Lua** embutidos, executados de forma **atômica** |
| **Persistência** | Pode persistir em **disco** |
| **Cache** | Dados em **memória**, com **expiração automática de chaves** e memória configurável |
| **Escalabilidade** | **Clusters** e **replicação** |
| **Comunidade** | Ativa, com atualizações frequentes |

- **Usos**: cache, **contadores em tempo real**, **filas de mensagens**, sessões, análise em tempo real. Segundo o resumo, é usado **principalmente (mas não somente)** para cache em aplicações distribuídas.

## Custos
O Redis é **gratuito** (código aberto), mas há custos de:
1. **Hospedagem própria**: servidores, rede, energia, refrigeração.
2. **Nuvem**: serviços gerenciados como **Amazon ElastiCache**, **Azure Cache for Redis** e **Google Cloud Memorystore**, com taxas de uso, armazenamento e transferência.
3. **Recursos adicionais**: segurança, monitoramento, escala automática, backups e replicação.

Recomenda-se uma **análise de custo-benefício**.

## Modelagem de dados
| Tipo de valor | O que é |
|---|---|
| **Strings** | O mais simples: uma sequência de caracteres |
| **Listas** | Sequência **ordenada**; inserção no início ou no fim |
| **Conjuntos** | Coleção **não ordenada** de elementos **únicos** |
| **Sorted Sets** | Como conjuntos, mas cada elemento tem um **score**, e são **classificados** por ele |
| **Hashes** | Mapeamento de **campos para valores**, como um dicionário |

- Também há **HyperLogLogs, Bitmaps e Streams**, para aplicações específicas.
- **Escolha da estrutura**: ex., **hashes** para informações de usuários (cada campo, um atributo); **listas** para listas de tarefas.
- Operações pela **Redis CLI** ou por bibliotecas de cada linguagem.

**Exemplo (Código 1)**:
```
"cpf:12345678900": "{\"name\": \"João da Silva\", \"age\": 30, \"email\": \"joao@example.com\"}"
"cpf:98765432100": "{\"name\": \"Maria Souza\", \"age\": 25, \"email\": \"maria@example.com\"}"
```

**Leitura complementar** (indicada no PDF): Redis Documentation · Introduction to Redis · "Redis: Overview, Use Cases and Advantages", de Gaurav Choudhary.

## Referências
Carlisle · Chang et al., *Bigtable* · George e Yu · Joshi, *Redis in Action* · Krishnan · Lazoti · Paniz · Pawan et al. · Radulovic e Vukotic · Redmond e Wilson · Sadalage e Fowler
