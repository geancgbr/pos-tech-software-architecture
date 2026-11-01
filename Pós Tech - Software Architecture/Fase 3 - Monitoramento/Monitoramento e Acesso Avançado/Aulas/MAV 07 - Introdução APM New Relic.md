---
tags: [pos-tech/fase-3, monitoramento, newrelic, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 7
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 7_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 07 - Introdução APM New Relic

← [[MAV 06 - Criando dashboards com DD]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 08 - Logs com New Relic]]

> [!summary] Em uma frase
> Uma introdução ao **[[New Relic]]**, comparado ao Datadog, com o **Agent do APM** em aplicações **.NET e NodeJS**. O texto do PDF trata do **[[Apdex]]**, o padrão da indústria para medir a **satisfação do usuário** com o **tempo de resposta**: varia de **0 a 1** e classifica as solicitações em **satisfeitas, tolerantes e frustradas**.

> [!note] O PDF é a aula 07, mas o cabeçalho interno diz "AULA 05". O mesmo descompasso aparece nas aulas 8, 9 e 10 (cabeçalhos "AULA 06", "07" e "08").

## Hands On (vídeo)
Implementar o **Agent do New Relic APM** nas aplicações **.NET e NodeJS**, por **container** e configuração de instrumentação. Segundo o "O que vem por aí", a partir das métricas se analisam **performance** e um **mapa da comunicação** entre as aplicações instrumentadas e as de terceiros. O Saiba Mais diz que "em vídeo vimos algumas métricas".

## Apdex
- **Padrão da indústria** para medir a satisfação do usuário com o **tempo de resposta** de aplicativos e serviços web. Segundo o PDF (citando a New Relic), é "uma solução simplificada de **SLA**", que mostra a satisfação por métricas como a **pontuação Apdex** e o **percentual de insatisfação**, em vez de métricas facilmente distorcidas, como o **tempo médio de resposta**.
- Definir um **limite útil** (o **Apdex T**) ajuda a ver a satisfação geral e obter a quantidade certa de rastreamento para resolver problemas (Figura 1).
- **Pontuação**: a proporção entre as solicitações **satisfeitas e tolerantes** e o **total**. Cada satisfeita conta **1**; cada tolerante conta **meia**.
- Varia de **0** (pior: 100% frustrados) a **1** (melhor: 100% satisfeitos).

| Categoria | Critério |
|---|---|
| **Satisfeitos** | Tempo de resposta **≤ T** |
| **Tolerantes** | **> T** e **≤ 4T** |
| **Frustrados** | **> 4T** ou **erro no servidor**. Qualquer erro do lado do servidor (como "500: Application Error") é frustrante, **independentemente da velocidade** |

- **Exemplo do PDF**: em 2 minutos, um host atende **200** solicitações, com **T = 0,5 s** (500 ms, valor arbitrário escolhido pelo usuário). **170** em até 500 ms (satisfeitas), **20** entre 500 ms e 2 s (tolerantes) e **10** acima de 2 s ou mal atendidas (frustradas).
  **Apdex = (170 + 20/2) / 200 = 0,9**.
- O **`apdex_f`** do arquivo de configuração é **quatro vezes** o Apdex T. É útil, por exemplo, no rastreamento da transação.
- Uma **alta taxa de erros** pode dar um tempo médio de resposta satisfatório, mas uma **pontuação Apdex baixa**.

> [!note] Ao explicar os tolerantes, o PDF dá "4 x 1,2 = 4,8 segundos" como tempo máximo tolerável, embora o exemplo anterior use T = 0,5 s.

**Faixas de cores**
| Faixa | Cor | Significado |
|---|---|---|
| **< 0,5** | Cinza | Além do crítico; **ação imediata** |
| **0,5 a 0,7** | Vermelho | Problemas críticos; **ação imediata** |
| **0,7 a 0,85** | Laranja | Tendendo a uma direção negativa; precisa de investigação |
| **0,85 a 0,95** | Azul | **A faixa ideal**: Apdex T bem ajustado e desempenho saudável |
| **0,95** (assim no PDF) | Azul | O Apdex T **pode estar alto demais** e a leitura não é precisa; considere **reduzir o Apdex T** |

- **O primeiro lugar a olhar** ao investigar uma falha é a pontuação Apdex: ela monitora a satisfação geral, combinando desempenho (tempo de resposta, taxas de transferência) e taxas de erros.

## Percentual de insatisfação (dissatisfaction percentage)
Calculado assim (como no PDF):
- `Frustrações(transação) + Tolerâncias(transação)/2`
- `Frustrações(App) + Tolerâncias(App)/2`

Uma transação **sempre lenta, mas raramente visitada**, contribui pouco para a insatisfação total. Já uma transação **normalmente rápida, mas com altas taxas de transferência**, pode contribuir muito, porque responde por grande parte do tráfego do aplicativo.

- O PDF também mostra um **Heat Map** de Apdex do **Dynatrace** (Figura 2).

## Referências
Grill (2018; a legenda da Figura 2 diz 2022), Dynatrace e ServiceNow · New Relic: Apdex: Meça a satisfação do usuário · Introdução ao New Relic para .NET · para Node.js · Solucionar problemas com a página de resumo do APM
