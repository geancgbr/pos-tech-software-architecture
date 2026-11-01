---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [Teste de carga, Testes de carga, Teste de estresse, Stress test, Load test]
---

# Teste de Carga e Teste de Estresse

Os dois são **testes de desempenho**. Diferem na **finalidade** e nos aspectos avaliados.

| | Carga | Estresse |
|---|---|---|
| Condição | **Uso normal**, com carga típica | **Extrema**, além dos limites |
| Avalia | Se o sistema lida com o **número esperado** de usuários e transações | A **capacidade máxima**, com carga excessiva e intensiva |
| Objetivo | **Gargalos**, **estabilidade**, requisitos de desempenho | **Pontos de falha**: recursos esgotados, tempo de resposta excessivo, comportamento inesperado |

**Benefícios do teste de carga**: melhora do desempenho · garantia da resiliência · prevenção de falhas (escalabilidade e capacidade).

Na aula 1, o teste de estresse aparece como um tipo de [[Teste de Caixa Branca e Caixa Preta|caixa preta]]: submete o software a condições extremas de carga, volume de dados ou interações simultâneas.

Ferramentas: [[Ferramentas de Teste de Carga (JMeter e K6)]]

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
- **Carga**: suportar o número **esperado** de usuários por um período estendido; **cenários de uso** e **ramp-up**; métricas de latência, throughput, erros (4xx, 5xx) e recursos.
- **Stress**: forçar **além dos limites**; **carga extrema** e **condições adversas** (desligar bancos ou serviços); tempo até uma taxa de falha, comportamento sob falha e **recuperação**.
- **Diferenças**: escopo (normal e picos × extremos), duração (**costumam** ser média ou longa × podem ser curtos) e foco ([[MS2 03 - Testando microsserviços]]).

Aparece em: [[QS 01 - Principais conceitos]], [[QS 06 - Testes de carga]], [[MS2 03 - Testando microsserviços]]
