---
tags: [pos-tech/fase-3, monitoramento, datadog, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 2
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 2_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 02 - Introdução APM Datadog

← [[MAV 01 - O que é APM e seus benefícios]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 03 - Logs com Datadog]]

> [!summary] Em uma frase
> A prática com o **[[Datadog]]** em aplicações **.NET** (com banco de dados) e **NodeJS**. Além de instrumentar no **mesmo host**, dá para instrumentar de forma **desacoplada**, com um **[[Sidecar]]**. O Datadog também gera métricas sobre os **status codes** das requisições.

## Hands On (vídeo)
"Nesta videoaula": implementar o **Agent do Datadog APM** nas aplicações **.NET e NodeJS**, por meio de **container** e da configuração de instrumentação. Segundo o "O que vem por aí", também se mostra **como ler a documentação oficial** e **personalizar a instrumentação**.

## Sidecar
- **Instrumentação no mesmo host** (como foi feito em aula) × **desacoplada**, a partir de **outro servidor/container**: isso é o **sidecar**.
- **Por que usar**: instrumentar de forma **transparente**, **sem usar os recursos da aplicação**, e **garantir o envio de erros**. Se a aplicação ou o container **"morrer"**, o erro **ainda é computado e enviado** ao Datadog.
- **Custo**: aumenta um pouco, porque fica **um host exclusivo para cada aplicação**. Sempre que uma aplicação sobe em container, **outro container** sobe como sidecar do Datadog para instrumentá-la.
- **Caso de uso** (frase do PDF): "utilizar sidecar somente para ambientes produtivos, ambientes de Staging e Development. É comum que a instrumentação seja feita no mesmo host para economizar". Ver a Figura 1 do PDF (Datadog Sidecar with K8s).

> [!note] A frase do caso de uso é ambígua no PDF: diz "somente para ambientes produtivos" e, na sequência, cita Staging e Development, onde seria "comum" instrumentar no mesmo host para economizar.

| Possibilidade com o Sidecar | O que o PDF diz |
|---|---|
| **Monitoramento de aplicações** | Desempenho em tempo real: **CPU, memória, latência de rede** |
| **Rastreamento distribuído** | Coletar e enviar o rastreamento de uma solicitação por vários **microsserviços**, mostrando a **jornada completa** |
| **Registro de logs** | Coletar e **centralizar logs**, para busca, análise, depuração e auditoria |
| **Análise de erros** | Coletar informações detalhadas dos erros e enviá-las para análise |
| **Monitoramento de infraestrutura** | Saúde dos contêineres, uso de recursos do host |

## Status codes
- O Datadog dá informações detalhadas sobre os **status codes** de cada request (**GET, POST, DELETE, OPTIONS**). Espera-se sempre **200 (OK)**, mas nem sempre acontece, e as informações do Datadog ajudam a corrigir (Figura 2).
- **Métricas de rastreamento**: **contagem de requisições, contagem de erros e latência**, calculadas com base em **100% do tráfego** da aplicação (visibilidade total).
- Dá para criar **dashboards e alertas** por status code, diferenciando **erros do cliente (4xx)** e **erros do servidor (5xx)**.
- Os status codes **sinalizam problemas** e dão **insights para prevenção e melhoria contínua**.
- **Levels** (Figura 3): indicam a **severidade** e se a request chegou ao destino. Segundo o PDF, um **level 500 "pode indicar que a request nem chegou ao destino"**; o **400** indica que **chegou, mas houve um erro**, como **não autorizado**: a request "bateu" no destino e foi **negada** (Figura 4, status 403).

> [!note] O PDF chama os 5xx de "erros do servidor", mas também diz que um level 500 "pode indicar que a request nem chegou ao destino".

## Referências
Datadog: Modern Application Performance Monitoring (APM) · MDN: HTTP response status codes · Red Hat: O que é o kernel Linux?
