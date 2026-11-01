---
tags: [pos-tech/fase-1, conceito]
aliases: [RF, RNF, Requisitos funcionais, Requisitos não funcionais]
---

# Requisitos Funcionais e Não Funcionais

- **Funcionais (RF)**: **o que** o sistema faz, ou seja, suas funções. Exemplos do CRM: cadastro de cotações, envio automático de follow-up, geração de proposta.
- **Não funcionais (RNF)**: **restrições e qualidades** para o sistema funcionar bem. Exemplos do CRM: 99% de disponibilidade, 100 usuários, 1000 propostas simultâneas, segurança, desempenho.

Fazem parte do documento da demanda, junto com persona, problema e jornada atual, objetivo e jornada da solução.

## Na disciplina Documentação de Arquitetura de Soluções
- **Funcionais**: **o que** o sistema deve fazer (ações, operações, comportamentos). Cada um deve ser **específico e testado**. Exemplos: login e perfil, processamento de pedidos, relatórios de vendas, transferência entre contas, carrinho e checkout.
- **Não funcionais**: **como** o sistema deve se comportar. Qualidades: desempenho, usabilidade, segurança, escalabilidade, confiabilidade (na aula 1 também disponibilidade e manutenibilidade). Exemplos: resposta em até 2 s, 10.000 usuários simultâneos, dados de pacientes criptografados em todas as transferências.
- **Levantamento**: hoje é **colaborativo** (PM, PO, time técnico, arquitetura), em vez de "coletar" tudo no início, como no modelo tradicional. Veja [[Arquiteto de Soluções]].
- **Boas práticas**: lista clara, linguagem objetiva, validação com os stakeholders, priorização, atualização constante, templates padronizados.
- Os RNF também definem benchmarks para testes de desempenho e segurança.

Detalhes: [[DOC 04 - Requisitos funcionais e não funcionais]]

Aparece em: [[DDD 07 - Levantamento de requisitos]], [[DOC 01 - Introdução à documentação de arquitetura]], [[DOC 04 - Requisitos funcionais e não funcionais]]
