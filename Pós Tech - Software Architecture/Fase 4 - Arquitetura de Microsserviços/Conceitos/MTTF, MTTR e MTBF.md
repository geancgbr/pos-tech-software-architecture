---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [MTTF, MTTR, MTBF, Mean Time to Failure, Mean Time to Repair, Mean Time Between Failures, Métricas de confiabilidade]
---

# MTTF, MTTR e MTBF

Métricas de confiabilidade (Figura 1 de [[RES 01 - Introdução à resiliência]]).

| Métrica | Definição | Exemplo do PDF |
|---|---|---|
| **MTTF** (Mean Time to Failure) | Tempo médio de funcionamento **antes** de um problema | 10 lâmpadas com 1.000 h em média → **1.000 h** |
| **MTTR** (Mean Time to Repair) | Tempo médio para **recuperar** depois da falha; quanto menor, melhor | Reparos de 2, 3 e 1 h → **2 h** |
| **MTBF** (Mean Time Between Failures) | **MTTF + MTTR**; quanto maior, mais confiável | 900 h + 100 h → **1.000 h** |

- Outras métricas da aula: **taxa de erros** (40 erros em 1.000 requisições = **4%**), **Coverage Factor**, **Reliability** e **Availability**.
- No Chaos Engineering, **MTBF** e **MTTR** medem o sucesso do programa; espera-se **redução do MTTR** ao longo do tempo ([[RES 05 - Chaos Engineering]]).

> [!note] Em [[RES 05 - Chaos Engineering]], MTTR é "Mean Time To **Recovery**".

Aparece em: [[RES 01 - Introdução à resiliência]], [[RES 05 - Chaos Engineering]]
