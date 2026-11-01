---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Microsserviços, Microservices, Microsserviço, Monolito distribuído, Padrões de microsserviços]
---

# Arquitetura de Microsserviços

Estilo de arquitetura que **decompõe funcionalmente** uma aplicação num conjunto de **serviços fracamente acoplados**, cada um com **sua própria API** e **seu próprio banco** (logicamente), evoluindo e escalando **de forma independente** ([[MS 01 - Estratégias e padrões de microsserviços]]).

- **Benefícios**: entrega e deployment contínuos (pipeline e squad por serviço) · serviços menores e mais fáceis de manter · escala independente · isolamento de falhas · novas tecnologias.
- **Desafios**: decomposição errada gera um **monolito distribuído** · complexidade de sistemas distribuídos (rede, falhas, transações e buscas entre serviços) · coordenação de publicação · decidir **quando** adotar (gradual; no início, não há problemas que os microsserviços resolvam).
- **Padrões**: em **3 camadas** (aplicação, infraestrutura de aplicação, infraestrutura) e domínios como decomposição, dados, consulta, consistência, comunicação, segurança, confiabilidade, observabilidade, API externa e descoberta.
- **Padrões da disciplina**: [[Estilos de Comunicação entre Serviços]], [[Circuit Breaker]], [[Descoberta de Serviços]], [[API Gateway]], [[Backend for Frontend (BFF)|BFF]], [[API Composition]], [[Banco de Dados por Serviço]], [[CQRS]], [[Saga]].

## Na disciplina Data Engineering
Cada serviço **pode** ter seu banco, de tipos diferentes, integrados por APIs; a consistência pode ser um desafio, e o [[ETL (Extract, Transform, Load)|ETL]] centraliza os dados ([[DE 07 - Bancos de dados e microsserviços]]). O termo passou a ser usado com mais frequência a partir de **2011**, com a **Netflix**.

Monolito: [[Arquitetura Monolítica]].

Aparece em: [[MS 01 - Estratégias e padrões de microsserviços]], [[DE 07 - Bancos de dados e microsserviços]]
