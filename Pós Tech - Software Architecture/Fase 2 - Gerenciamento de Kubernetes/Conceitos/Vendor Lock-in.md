---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [vendor lock-in, Lock-in]
---

# Vendor Lock-in

O PDF não define o termo: descreve um cenário e conclui "Isso é o vendor lock-in". Ou seja, instrumentar com o agente e a API proprietária de um fornecedor obriga, para migrar, a remover e reescrever toda a instrumentação, o que é **caro, demorado e arriscado**.

**O cenário da aula**: todos os microsserviços instrumentados com o **agente e a API proprietária** do Fornecedor A. Para migrar para o Fornecedor B (melhor e mais barato), seria preciso **remover toda a instrumentação e reescrever** com a API do B, em dezenas ou centenas de serviços.

**A solução do OpenTelemetry**: um **padrão unificado**. Instrumenta-se **uma vez** com a API do OTel e configura-se um **exportador** para qualquer back-end compatível: trocar de fornecedor vira **uma mudança de configuração, não uma reescrita de código**. Com o [[OpenTelemetry Collector]], basta mudar a configuração do Coletor, sem novo deploy da aplicação (aula 5).

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 05 - Boas práticas e desafios]]
