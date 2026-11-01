---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Contextos Delimitados, Bounded Context, Bounded Contexts]
---

# Contexto Delimitado

**Limite que impomos ao modelo de domínio.** Dentro dele, termos, definições, propriedades e operações compartilham **uma única [[Linguagem Ubíqua]]**.

- **Não é a mesma coisa que subdomínio.** Os limites saem da análise do negócio, não da lista de [[Subdomínios]].
- **Tamanho**: não há regra. Use a linguagem ubíqua como métrica:
  - mesma terminologia e processos parecidos → talvez juntar;
  - muito distintos → separar.
- Pode existir um único contexto para a solução inteira (se ela for pequena) ou uma relação 1 para 1 (em sistemas grandes e complexos).
- **Times**: um contexto é sempre de **um único time**, nunca dividido entre dois. Um time pode cuidar de vários contextos. O número de contextos dá uma ideia do número de times.
- Mais gente não acelera um contexto com muitas dependências internas.
- No [[Event Storming]], os **eventos pivotais** indicam onde estão os limites.

Como os contextos se relacionam: [[Padrões de Integração entre Contextos]] e [[Mapa de Contexto]].

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
Cada subdomínio deve ter **seu próprio modelo e linguagem**; em microsserviços, **cada serviço pode encapsular um Bounded Context** específico ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]).

Aparece em: [[DDD 03 - Descoberta e formação do conhecimento]], [[DDD 04 - Trabalhando com contextos delimitados]], [[DDD 06 - Event Storming]], [[MS2 02 - Aplicando a lógica de negócios no microsserviço]]
