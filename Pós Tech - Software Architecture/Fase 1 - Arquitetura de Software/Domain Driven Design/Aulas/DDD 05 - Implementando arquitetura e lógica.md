---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 5
fonte: "Aula 05- Implementando arquitetura e lógica.pdf"
---

# DDD 05 - Implementando arquitetura e lógica

← [[DDD 04 - Trabalhando com contextos delimitados]] · [[Domain Driven Design]] · Próxima → [[DDD 06 - Event Storming]]

> [!summary] Em uma frase
> Aqui começa o [[Design Tático]], o "como": a arquitetura em [[Camadas do DDD|4 camadas]] e os blocos de construção ([[Objeto de Valor]], [[Entidade]], [[Agregado]] e [[Serviço de Domínio]]).

## Estratégico × tático
| | [[Design Estratégico]] (aulas 1–4) | [[Design Tático]] (aula 5) |
|---|---|---|
| Pergunta | O quê? Por quê? | Como? |
| Produz | Domínio, subdomínios, linguagem ubíqua, contextos e mapa | Arquitetura, tecnologias, modelo de domínio |
| Exemplos de decisão | Saber o que queremos fazer e por quê, para entender aonde queremos chegar | Banco relacional ou NoSQL? Microsserviços ou barramento de serviços? |

## As 4 camadas
1. **Interface de Usuário**: GUI, CLI e APIs para integração com outros sistemas.
2. **Aplicação**: faz a mediação entre a interface e o domínio e organiza as tarefas. Não tem regra de negócio.
3. **Domínio**: o "coração do software" (Evans), com as regras de negócio e as mudanças de estado.
4. **Infraestrutura**: persistência, mensageria e suporte técnico às outras camadas.

O esquema visual está na Figura 1 do PDF. Detalhes em [[Camadas do DDD]].

## Blocos de construção
| | [[Objeto de Valor]] | [[Entidade]] |
|---|---|---|
| Identidade | Não tem. É distinguido pelos **valores** | Tem um **ID único**, nunca reutilizado |
| Mutabilidade | **Imutável**: se algo muda, cria-se outro | **Mutável** |
| Igualdade | Por valor | Por ID |
| Inserir algo repetido | Não entra, porque já existe | Entra, porque ganha um ID novo |

- **[[Agregado]]**: conjunto de entidades e objetos de valor com uma **fronteira**. Tem **consistência forçada**: só a lógica do próprio agregado altera o estado dele. Quem está fora pode ler e pode pedir mudanças por **comandos**.
- **[[Serviço de Domínio]]**: lógica que trabalha com várias entidades e agregados (cálculos, rotinas).

## Exemplo da escola
- **Aplicação**: rotina que contabiliza as faltas do dia (em tempo real ou em lote). Ela só dispara a lógica de presença e devolve o resultado.
- **Domínio**: regra da nota com desconto por entrega atrasada, regras dos planos de aula.
