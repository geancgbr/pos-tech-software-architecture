---
tags: [pos-tech/fase-4, microsservicos, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 2
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 2.pdf"
---

# MS2 02 - Aplicando a lógica de negócios no microsserviço

← [[MS2 01 - Desenhando a lógica de negócios com microsserviços]] · [[Estrutura de Microsserviços Parte II]] · Próxima → [[MS2 03 - Testando microsserviços]]

> [!summary] Em uma frase
> Organizar a lógica de negócio com os padrões **Domain Model** e **Aggregate**, que resolve problemas de **concorrência**. O texto do PDF trata dos bloqueios **Pessimistic** e **Optimistic Offline Lock** ([[Offline Lock (Pessimista e Otimista)]]), do **DTO**, do **DDD** aplicado a microsserviços e do **ORM**.

> [!note] O título do PDF é "Aplicando a lógica de negócios no nosso microsserviço - Parte 2".

## Hands On
- Testar o **Catálogo de Produtos** com o padrão de **Domínio** e ver o que acontece ao **alterar os preços** de um conjunto de produtos **ao mesmo tempo**.
- Aplicar o padrão de **Agregação** para lidar com a **concorrência** e evitar inconsistências.
- **Para rodar**: repositório da aula 2, **MySQL Workbench** e **Postman**.
- Segundo o resumo, o **Domain Model** relaciona cada funcionalidade à sua **entidade**, e o **Aggregate** faz com que toda alteração em entidades e **value objects** seja **versionada a partir da entidade principal** do Aggregate. Ver [[Agregado]].

## Pessimistic × Optimistic Offline Lock
| | Pessimistic Offline Lock | Optimistic Offline Lock |
|---|---|---|
| Como funciona | **Uma transação de negócio por vez** acessa os dados: a transação **adquire um bloqueio** antes de usar o dado e, na maioria das vezes, termina sem interrupção | Antes do **commit**, verifica se os dados **mudaram** desde a leitura; se houver conflito, a transação é **revertida**. Assume que **conflitos são raros** |
| Exemplo do PDF | **Sistema bancário**: numa transferência, a conta fica bloqueada até o fim, evitando saldos incorretos | **Reserva de assentos**: todos tentam; no commit, verifica-se se o assento ainda está livre; se não, reverte e avisa o usuário |
| Vantagens | **Evita conflitos** (acesso exclusivo) · **previsibilidade** | **Alta concorrência** · **desempenho** (sem gerenciar bloqueios) |
| Desvantagens | **Baixa concorrência** · **desempenho** (**potencial** para esperas mais longas) | **Conflitos** e retrabalho em alta competição · **complexidade** (exige padrões como **Aggregate**) · **experiência do usuário** (reversões frequentes) |

## DTO (Data Transfer Object)
- Padrão para **transferir dados** entre componentes. Em microsserviços, é **frequentemente** usado para estruturar as **mensagens** enviadas pela rede, fáceis de **serializar e deserializar**. Ver [[DAO e DTO]].
- **Vantagens**: **desacoplamento** (sem conhecer o modelo de domínio do outro serviço) · **eficiência** · **validação** (**pode conter** lógica de validação antes da de negócio).
- **Desvantagens**: **mapeamento** entre domínio e DTO · **manutenção** quando o modelo muda.
- Mantém validação e transformação **separadas da lógica de negócio**.

## DDD em microsserviços
| Conceito | O que o PDF diz |
|---|---|
| **Bounded Contexts** | Sugere que cada subdomínio **deve ter** **seu modelo e sua linguagem**; cada serviço pode encapsular **um Bounded Context**. Ver [[Contexto Delimitado]] |
| **Aggregates** | Grupos de **entidades e objetos de valor** tratados como **uma unidade**; um Aggregate pode ficar **dentro de um único serviço**, ajudando na consistência. Ver [[Agregado]] |
| **Linguagem Ubíqua** | Linguagem comum entre devs e stakeholders; fundamental com equipes diferentes. Ver [[Linguagem Ubíqua]] |
| **Consistência eventual e comunicação assíncrona** | Padrões como **Event Sourcing** e **CQRS** ([[CQRS]]) |
| **Isolamento e desacoplamento** | Isolar o domínio da lógica de aplicativo e infraestrutura |

- **Vantagens**: foco no domínio · escalabilidade e manutenção.
- **Desvantagens**: **complexidade** (pode não ser necessário em domínios simples) · **custo inicial alto**. Ver [[O que é DDD]].

## ORM (Object-Relational Mapping)
Técnica que **mapeia objetos do domínio para um banco relacional**.

| Vantagens | Desvantagens |
|---|---|
| **Abstração** (objetos em vez de SQL puro) | **Performance** em leituras e escritas complexas (latência e throughput) |
| **Desacoplamento** do esquema | **Acoplamento à tecnologia** da biblioteca ORM |
| **Produtividade** (migrações automáticas, gerenciamento de sessão) | **Transações distribuídas** entre serviços (padrões como **Saga**) |
| **Consistência** entre o modelo de domínio e o esquema (útil com DDD) | — |

## Referências
Ambler e Sadalage, *Refactoring Databases* · Fowler: DDD_Aggregate · Domain Model · Optimistic Offline Lock · Pessimistic Offline Lock · Richardson, *Microservices Patterns*
