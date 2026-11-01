---
tags: [pos-tech/fase-3, monitoramento, newrelic, conceito]
aliases: [Apdex score, Apdex T, apdex_f]
---

# Apdex

**Padrão da indústria** para medir a **satisfação do usuário** com o **tempo de resposta** de aplicativos e serviços web ([[MAV 07 - Introdução APM New Relic]]).

- **Pontuação** = (satisfeitas + tolerantes/2) / total, de **0** (100% frustrados) a **1** (100% satisfeitos).
- **Satisfeitos**: ≤ T · **Tolerantes**: > T e ≤ 4T · **Frustrados**: > 4T **ou erro no servidor** (sempre frustrante, por mais rápido que seja).
- **Exemplo**: 200 solicitações, T = 0,5 s; 170 satisfeitas, 20 tolerantes, 10 frustradas → **(170 + 20/2)/200 = 0,9**.
- **`apdex_f`** = 4 × Apdex T.
- **Cores**: < 0,5 cinza · 0,5 a 0,7 vermelho · 0,7 a 0,85 laranja · **0,85 a 0,95 azul (ideal)** · 0,95 azul (T talvez alto demais; considerar reduzir).
- **Primeiro lugar a olhar** ao investigar uma falha. Uma alta taxa de erros pode ter tempo médio bom e Apdex baixo.
- **Percentual de insatisfação**: Frustrações + Tolerâncias/2, por transação e por aplicação. Uma transação normalmente rápida, mas com **altas taxas de transferência**, **pode** contribuir muito, por responder por grande parte do tráfego.
- **Nos mapas** e gauges: as cores de saúde dos Service Maps podem se basear no Apdex ([[MAV 12 - Contexto Map New Relic]]), e gauges acompanham o Apdex score ([[MAV 11 - Criando dashboards com New Relic]]).

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
Apdex (**Application Performance Index**): satisfeitas (ex.: até **3 s**), toleradas (3 a 12 s), frustradas (acima de 12 s **ou com falha**, erros **4xx, 5xx**). Fórmula: (Satisfeitas + 0,5 × Toleradas) / Total. Interpretação de exemplo: 0 a 0,49 pobre · 0,5 a 0,69 justo · 0,7 a 0,84 bom · **0,85 a 0,94 excelente** · 0,95 a 1 excepcional ([[MS2 03 - Testando microsserviços]]).

Aparece em: [[MAV 07 - Introdução APM New Relic]], [[MS2 03 - Testando microsserviços]]
