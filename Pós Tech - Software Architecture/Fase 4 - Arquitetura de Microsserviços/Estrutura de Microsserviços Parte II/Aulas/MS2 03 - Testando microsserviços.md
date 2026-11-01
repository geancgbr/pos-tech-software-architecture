---
tags: [pos-tech/fase-4, microsservicos, testes, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 3
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 3.pdf"
---

# MS2 03 - Testando microsserviços

← [[MS2 02 - Aplicando a lógica de negócios no microsserviço]] · [[Estrutura de Microsserviços Parte II]] · Próxima → [[MS2 04 - Testando microsserviços, parte 2]]

> [!summary] Em uma frase
> Os tipos de teste de um serviço, com foco nos **testes unitários**. O texto do PDF trata do **[[TDD (Test-Driven Development)|TDD]]** em microsserviços, dos **[[Teste de Carga e Teste de Estresse|testes de carga e de stress]]** e do **[[Apdex]]** como métrica de satisfação.

## Hands On
Ver os **testes unitários** do **Catálogo de Produtos**: criar **mocks** para as dependências do **`CatalogoService`**, executar os testes, **simular bugs** e gerar **relatórios**. Repositório da aula 3. Segundo o resumo, a aula trata dos **tipos de testes** e seus escopos, dos testes unitários **solitários e sociáveis** e de **mocks e stubs**, que diminuem a complexidade e focam os testes na funcionalidade alvo. Ver [[Mock]].

## TDD
- Técnica em que **o teste é escrito antes do código**. **Ajuda a** garantir que o código faz o que deve, dá **feedback** e facilita mudanças futuras.
- **Ciclo**: (1) **escrever o teste** da nova funcionalidade; (2) **executar**, e ele **deve falhar**; (3) escrever o **código mínimo** para passar; (4) **refatorar**, mantendo a funcionalidade.
- Útil em microsserviços, que são **isolados** e testados de forma **independente**, e se encaixa nos pipelines de **CI/CD**. Exige **investimento inicial de tempo**, com retorno em **menos bugs** e manutenção mais fácil.

## Testes de carga × testes de stress
| | Teste de carga | Teste de stress |
|---|---|---|
| Objetivo | Verificar se o sistema suporta o número **esperado** de usuários e transações simultâneas por um **período estendido** | **Forçar além dos limites** para achar os **pontos de falha** e o comportamento em condições extremas |
| Estratégias | **Cenários de uso** realistas · **Ramp-up** (aumentar a carga aos poucos) | **Carga extrema** (bem acima do pico) · **Condições adversas** (desligar bancos ou serviços dependentes) |
| Métricas | **Latência** (ex.: tempo médio de resposta) · **Throughput** (ex.: requisições por segundo) · **Erros** (ex.: 4xx, 5xx) · **Recursos** (ex.: CPU, memória) | **Tempo até uma taxa de falha** (ex.: 1 minuto até 5% de falhas) · **Comportamento sob falha** (ex.: vazamento de memória, lentidão, restart) · **Recuperação** (ex.: voltou ao normal com resposta média de 10 s) |
| Escopo | Condições **normais e picos** | Condições **extremas e limites** |
| Duração | **Costumam** ser de **média ou longa** duração (simular uso real) | Podem ser **curtos** (avaliar limites) |

- Ambos avaliam métricas semelhantes, mas o stress foca em **onde falha e como se recupera**.

## Apdex (Application Performance Index)
- Métrica **padrão** de **satisfação** com o desempenho: um índice **simples, numérico e padronizado**. Útil em microsserviços, onde vários serviços contribuem para a experiência.

| Categoria | Exemplo do PDF |
|---|---|
| **Satisfeitas** | Até **3 s** |
| **Toleradas** | Entre **3 e 12 s** |
| **Frustradas** | Acima de **12 s** ou **com falha** (erros **4xx, 5xx** etc.) |

- **Fórmula**: (Satisfeitas + 0,5 × Toleradas) / Total, entre **0 e 1**.
- **Interpretação de exemplo**: **0 a 0,49** pobre · **0,5 a 0,69** justo · **0,7 a 0,84** bom · **0,85 a 0,94** excelente · **0,95 a 1** excepcional.
- **Vantagens**: simplicidade · **padronização** (comparar serviços ou versões) · **foco no usuário**. Pode ser uma adição importante à **observabilidade**.

> [!note] Na disciplina Monitoramento e Acesso Avançado (Fase 3, aula 7), as faixas de cor do Apdex são outras (0,85 a 0,95 é a faixa "ideal"), e os frustrados são as respostas acima de 4T **ou com erro no servidor**; aqui, entram também os erros **4xx**.

> [!note] O "O que vem por aí" e o resumo tratam dos tipos de teste (unitários solitários e sociáveis, mocks e stubs); o Saiba Mais trata de TDD, testes de carga e stress e Apdex.

## Referências
Clemson, *Testing Strategies in a Microservice Architecture* (2014) · Fowler: Mocks Aren't Stubs · TestDouble · TestPyramid · UnitTest · Richardson, *Microservices Patterns*
