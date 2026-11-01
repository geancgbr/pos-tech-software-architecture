---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Fallback, Graceful Degradation, Degradação graciosa, fallbackMethod]
---

# Fallback e Graceful Degradation

- **Graceful Degradation**: continuar com as funcionalidades **essenciais** mesmo com partes degradadas. É **preventivo**, ativado automática ou manualmente (muitas vezes por **feature toggles**) ([[RES 02 - Padrões de resiliência]]).
- **Fallback**: age **depois** que o problema ocorreu ([[RES 02 - Padrões de resiliência]]). No [[Resilience4j]], é chamado **automaticamente** com o circuito **aberto** ou numa **exceção**; permite resposta padrão, caminho alternativo ou logar e alertar; `fallbackMethod` recebe a exceção ou nenhum parâmetro ([[RES 03 - Resiliência na prática]]).
- Retries **assíncronos** podem ser uma alternativa de fallback ([[RES 02 - Padrões de resiliência]]); o Timeout pode acionar um fallback ([[RES 03 - Resiliência na prática]]).

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]]
