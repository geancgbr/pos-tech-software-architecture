---
tags: [pos-tech/fase-4, microsservicos, revisao]
disciplina: Estrutura de Microsserviços Parte II
---

# Revisão - Estrutura de Microsserviços Parte II

[[Estrutura de Microsserviços Parte II]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Lógica de negócio
> [!question]- O que é um high-level domain model, e quais os componentes típicos?
> Uma visão de como os serviços se relacionam e contribuem para os objetivos de negócio. Componentes: entidades, serviços, relações e eventos. → [[MS2 01 - Desenhando a lógica de negócios com microsserviços]]

> [!question]- Cite desafios da decomposição em serviços.
> Limites dos domínios, granularidade, comunicação, transações e consistência (SAGA, Transaction Outbox, Event Sourcing), descoberta, segurança, monitoramento, testes e DevOps.

> [!question]- Serviços muito granulares × muito abrangentes?
> Muito granulares: overhead de comunicação. Muito abrangentes: baixa coesão e alta complexidade.

> [!question]- O que é o DAO, e por que usá-lo em microsserviços?
> Um padrão que encapsula o acesso à fonte de dados, separando-o da lógica de negócio: desacoplamento, reusabilidade (DRY), testabilidade e consistência no CRUD. → [[DAO e DTO]]

## Aula 2 - Domain Model e Aggregate
> [!question]- Pessimistic × Optimistic Offline Lock?
> Pessimista: bloqueia o dado antes de usar (uma transação por vez; ex.: sistema bancário). Otimista: verifica conflitos no commit e reverte (alta concorrência; ex.: reserva de assentos). → [[Offline Lock (Pessimista e Otimista)]]

> [!question]- Para que serve o DTO?
> Transferir dados entre componentes, estruturando as mensagens entre serviços, com desacoplamento, eficiência na serialização e validação.

> [!question]- Como o DDD se aplica a microsserviços?
> Cada serviço pode encapsular um Bounded Context; um Aggregate pode ficar num único serviço; linguagem ubíqua; Event Sourcing e CQRS para consistência eventual; isolamento do domínio.

> [!question]- Vantagens e desvantagens do ORM?
> Vantagens: abstração, desacoplamento, produtividade, consistência com o domínio. Desvantagens: performance, acoplamento à biblioteca e transações distribuídas.

## Aula 3 - Testes
> [!question]- Qual o ciclo do TDD?
> Escrever o teste, executá-lo (deve falhar), escrever o código mínimo para passar e refatorar. → [[TDD (Test-Driven Development)]]

> [!question]- Teste de carga × teste de stress?
> Carga: o volume esperado por um período estendido (cenários, ramp-up). Stress: além dos limites, para achar o ponto de falha e a recuperação (carga extrema, condições adversas). → [[Teste de Carga e Teste de Estresse]]

> [!question]- Qual a fórmula do Apdex e os limites do exemplo?
> (Satisfeitas + 0,5 × Toleradas) / Total; satisfeitas até 3 s, toleradas de 3 a 12 s, frustradas acima de 12 s ou com falha. → [[Apdex]]

## Aula 4 - Testes, parte 2
> [!question]- Continuous Delivery × Continuous Deployment, segundo a aula?
> Delivery: automatiza a implantação de um commit aprovado. Deployment (Publicação Contínua): toda mudança que passa nos testes vai para produção sem aprovação de alguém.

> [!question]- Quais métricas de qualidade de código o PDF cita?
> Complexidade ciclomática, débito técnico e cobertura de testes.

> [!question]- SAST × DAST?
> SAST: analisa o código-fonte sem executar. DAST: analisa o app em execução, simulando ataques.

> [!question]- Como o BDD escreve os cenários?
> Em linguagem natural, frequentemente com Gherkin: Given (contexto), When (ação), Then (resultado). → [[BDD (Behavior-Driven Development)]]

> [!question]- O que o resumo diz sobre os testes de ponta a ponta?
> Podem ser custosos, dada sua fragilidade e complexidade; é estratégico focar nas jornadas de usuário mais importantes.

## Aula 5 - Deploy
> [!question]- Como proteger dados em repouso e em trânsito?
> Em repouso: algoritmos robustos como AES e RSA. Em trânsito: TLS (HTTPS). Chaves em soluções robustas, por exemplo um cofre de senhas, com rotação. → [[Criptografia e mTLS]]

> [!question]- O que é o mTLS?
> Autenticação bidirecional com certificados digitais (Client Authentication do TLS), que verifica a identidade das duas partes.

> [!question]- Blue-Green × Canary × Shadow?
> Blue-Green: duas versões em paralelo e troca do tráfego. Canary: a nova versão para uma porcentagem dos usuários. Shadow: cópia do tráfego real para a nova versão, sem expô-la. → [[Estratégias de Deployment]]

> [!question]- Recreate × Rolling Update?
> Recreate: remove todas as instâncias antigas antes das novas (tolera inatividade). Rolling Update: substitui gradualmente, uma a uma ou em lotes.

## Aula 6 - Observabilidade
> [!question]- Warning × alert?
> Warning: um aviso de que algo pode estar errado, que dá tempo ao time de agir. Alert: algo definitivamente deu errado. → [[MS2 06 - Realizando o deploy de microsserviços, parte 2]]

> [!question]- Cite boas práticas do OpenTelemetry da aula.
> Dados contextuais nos traces, padrões de nomenclatura e amostragem (ex.: 50%) para reduzir custos. → [[OpenTelemetry]]

> [!question]- Como se calcula o Error Budget?
> Error Budget = 100% − SLO (ex.: 98% de disponibilidade → 2%). → [[Error Budget]]

## Dúvidas em aberto
- Aulas 3, 4 e 5: o "O que vem por aí" e o resumo tratam de temas diferentes do Saiba Mais.
- Aula 3: as faixas do Apdex e o critério de frustradas diferem dos da Fase 3 (aula 7 de Monitoramento e Acesso Avançado).
- Aula 6: no exemplo financeiro, os pedidos são contados por semana, mas o budget é dado "por mês".

## Pontos fracos (o que errei)
