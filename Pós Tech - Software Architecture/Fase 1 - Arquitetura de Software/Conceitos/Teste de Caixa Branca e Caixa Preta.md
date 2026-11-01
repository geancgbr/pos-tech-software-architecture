---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [Caixa branca, Caixa preta, White Box, Black Box, Teste de caixa branca, Teste de caixa preta]
---

# Teste de Caixa Branca e Caixa Preta

Duas abordagens com o mesmo objetivo (qualidade), que diferem na **perspectiva** e no **nível de conhecimento interno** do sistema.

## Caixa branca (White Box)
Feito **com conhecimento da estrutura interna e do código-fonte**. A pessoa testadora acessa o código e a lógica, o que permite uma avaliação mais detalhada e direcionada.

| Tipo | O que verifica |
|---|---|
| **Cobertura de código** | Se todas as partes do código foram executadas e testadas, medindo a cobertura de instruções, ramos (condicionais) e caminhos |
| **Fluxo de controle** | Se todas as decisões lógicas e caminhos possíveis do fluxo de controle foram testados |
| **Caminho básico** | Todas as combinações possíveis de caminhos pelo código, para cobrir todos os fluxos de execução |
| **Integração** | Se os diferentes componentes funcionam corretamente em conjunto |

## Caixa preta (Black Box)
Feito **sem conhecimento detalhado do código-fonte ou da estrutura interna**. O foco é exclusivo em **entradas e saídas**, avaliando o comportamento e a funcionalidade como um todo, com base nos **requisitos funcionais e nas especificações**.

| Tipo | O que avalia |
|---|---|
| **Funcional** | Se atende aos requisitos funcionais, comparando as saídas esperadas com as obtidas para diferentes entradas |
| **Usabilidade** | Facilidade de uso, intuitividade e eficiência para o usuário final |
| **Desempenho** | Tempo de resposta, capacidade de processamento, consumo de recursos e escalabilidade |
| **Segurança** | Vulnerabilidades e medidas de proteção adequadas |
| **Estresse** | Comportamento e estabilidade sob condições extremas de carga, volume de dados ou interações simultâneas |

Na aula 1, o teste de integração aparece como caixa branca. Ele é aprofundado em [[Teste de Integração]]. O teste de estresse é aprofundado em [[Teste de Carga e Teste de Estresse]].

Aparece em: [[QS 01 - Principais conceitos]]
