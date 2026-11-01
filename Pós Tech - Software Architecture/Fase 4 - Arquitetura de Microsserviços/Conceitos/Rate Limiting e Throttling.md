---
tags: [pos-tech/fase-4, microsservicos, resiliencia, conceito]
aliases: [Rate Limiting, Rate Limiter, Throttling, Token Bucket]
---

# Rate Limiting e Throttling

| | **Rate Limiting** | **Throttling** |
|---|---|---|
| O que faz | Controla **quantas requisições** são processadas por período; muito usado em APIs públicas; garante experiências mais **justas** | Ajusta **dinamicamente** a taxa conforme a **carga**; mais adaptável |
| Como | **Token Bucket** (sem tokens, negar ou enfileirar); **comumente** com NGINX ou Redis | Reduz as requisições ou retorna **429 Too Many Requests** |
| Exemplo | 100 requisições por minuto por cliente | Streaming que reduz qualidade ou conexões em picos |
| Prós | Protege contra **DDoS**; mantém os serviços sob alta demanda | Protege contra sobrecarga; mantém o essencial |
| Contras | **Pode** frustrar usuários legítimos | **Pode** degradar operações não críticas |

- O Throttling é **frequentemente** usado junto com o Rate Limiting ([[RES 02 - Padrões de resiliência]]). O Rate Limiter também aparece nas videoaulas com [[Resilience4j]] ([[RES 03 - Resiliência na prática]]).

Aparece em: [[RES 02 - Padrões de resiliência]], [[RES 03 - Resiliência na prática]]
