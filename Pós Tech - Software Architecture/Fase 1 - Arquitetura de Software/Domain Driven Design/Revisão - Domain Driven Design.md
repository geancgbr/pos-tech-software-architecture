---
tags: [pos-tech/fase-1, ddd, revisao]
disciplina: Domain Driven Design
---

# Revisão - Domain Driven Design

[[Domain Driven Design]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- DDD é uma metodologia de projeto?
> Não. É uma cultura de comunicação e documentação entre time e negócio, para que a solução "fale a língua do negócio". → [[O que é DDD]]

> [!question]- Qual a diferença entre design estratégico e design tático?
> Estratégico é o **o quê e por quê** (domínio, subdomínios, linguagem, contextos). Tático é o **como** (camadas, entidades, VOs, agregados). → [[Design Estratégico]] · [[Design Tático]]

> [!question]- Classifique para uma escola: aulas e metodologias, gestão de dados de pais, criptografia dos dados.
> Principal · Suporte · Genérico. → [[Subdomínios]]

> [!question]- O que caracteriza um subdomínio de suporte, e em que ele difere do genérico?
> O de suporte apoia e complementa o principal, tem lógica simples (geralmente CRUD) e não dá vantagem estratégica. O genérico é o conjunto de processos comuns no mercado (portal, loja on-line, autenticação): é naturalmente complexo, mas não diferencia o produto ou serviço.

> [!question]- Quem é o Domain Expert?
> Quem detectou a necessidade e conhece o negócio a ponto de descrever os processos: quem conta a história. Há vários por domínio. → [[Domain Expert]]

## Aula 2 - Domain Storytelling
> [!question]- Quais são os elementos da linguagem pictográfica?
> Atores, objetos de trabalho, atividades (setas), números sequenciais, anotações, grupos e cores. Além deles: cenários e escopo. → [[Domain Storytelling]]

> [!question]- Por que não se usam if/else nem loopbacks nas atividades?
> Para focar no fluxo e na intenção do ator. Cada condicional vira **outra história** (cenário), e retornos ficam para técnicas como BPMN.

> [!question]- Como nomear um ator?
> Pela **função** (Professor, Secretaria), nunca pelo nome da pessoa.

> [!question]- O que são AS IS e TO BE?
> AS IS é a realidade de hoje. TO BE é o desejo, o processo futuro. O expert mistura os dois ao contar, então é preciso separar.

> [!question]- Quais papéis compõem a equipe?
> Domain Experts, ouvintes, moderador e modelador.

## Aula 3 - Descoberta e formação do conhecimento
> [!question]- O que é linguagem ubíqua e onde ela vale?
> A terminologia real do negócio, compartilhada por negócio e time e usada no código. Vale **dentro de um contexto delimitado**. → [[Linguagem Ubíqua]]

> [!question]- Dê um exemplo de mesmo termo com significados diferentes em áreas diferentes.
> "Pais" para admissão, marketing e secretaria.

> [!question]- Contexto delimitado é a mesma coisa que subdomínio?
> Não. Os limites saem da análise do negócio e da linguagem ubíqua, não da lista de subdomínios. → [[Contexto Delimitado]]

> [!question]- Um contexto pode ser dividido entre dois times?
> Não. Um contexto pertence a um único time, mas um time pode ter vários contextos.

> [!question]- Qual a melhor métrica para decidir juntar ou separar contextos?
> A linguagem ubíqua: mesma terminologia e processos parecidos → juntar; muito distintos → separar.

## Aula 4 - Integração de contextos
> [!question]- Upstream e downstream na integração de contextos?
> Upstream é o fornecedor, que provê o serviço. Downstream é o cliente, que consome. → [[Upstream e Downstream]]

> [!question]- Por que o kernel compartilhado é desencorajado, e quando é inevitável?
> Porque fere os limites dos contextos: código comum entre times, e toda mudança afeta e precisa ser testada em todos. É inevitável em legado/monólito durante a modernização.

> [!question]- Conformista × ACL × OHS: qual a diferença?
> Conformista: o cliente aceita o modelo do fornecedor. ACL: o cliente traduz o modelo do fornecedor para o seu. OHS: o fornecedor expõe um protocolo aberto e estável para os clientes. → [[Padrões de Integração entre Contextos]]

> [!question]- Cite os 3 cenários em que se recomenda uma ACL.
> 1) O cliente tem um subdomínio principal. 2) O modelo do fornecedor é ineficiente ou incompleto (legado). 3) O fornecedor muda o protocolo com frequência.

> [!question]- O que a linguagem publicada acrescenta ao OHS?
> Uma abstração na linguagem de cada cliente (versões personalizadas), mantendo o protocolo aberto. Exemplos: adquirentes, EDI na logística.

> [!question]- Quando faz sentido usar caminhos separados?
> Quando integrar custa mais que duplicar, ou os times não conseguem se comunicar. Exemplos: relatórios, autenticação, logs.

> [!question]- O que fazer com uma grande bola de lama?
> Cercá-la com uma linha de limite, não aplicar modelagem sofisticada e impedir que contamine outros contextos.

> [!question]- O mapa de contexto é um artefato estático?
> Não. É um documento vivo, atualizado constantemente. → [[Mapa de Contexto]]

## Aula 5 - Design tático
> [!question]- Quais são as 4 camadas do DDD, e qual delas tem as regras de negócio?
> Interface de Usuário, Aplicação, Domínio e Infraestrutura. As regras ficam no **Domínio**, o "coração do software". → [[Camadas do DDD]]

> [!question]- A camada de aplicação pode ter regra de negócio?
> Não. Ela orquestra e dispara rotinas (por exemplo, a contabilização diária de faltas), sem alterar o estado nem conter regra.

> [!question]- A camada de domínio persiste dados?
> Não. Ela entrega as informações para a infraestrutura registrar.

> [!question]- Objeto de valor × entidade (identidade, mutabilidade, igualdade)?
> VO: sem ID, imutável, comparado por valor, substituído por inteiro. Entidade: ID único, mutável, comparada por ID. → [[Objeto de Valor]] · [[Entidade]]

> [!question]- O que é a consistência forçada de um agregado?
> Só a lógica do próprio agregado altera o estado dele. Quem está fora pode ler e pedir mudanças por comandos. → [[Agregado]]

> [!question]- Quando usar um serviço de domínio?
> Quando a lógica de domínio envolve várias entidades ou agregados (cálculos, rotinas). → [[Serviço de Domínio]]

## Aula 6 - Event Storming
> [!question]- Qual é a ordem das etapas?
> Brainstorming → linha do tempo → pontos de atenção → eventos pivotais → comandos e atores → políticas → modelos de leitura → sistemas externos → agregados → contextos. → [[Event Storming]]

> [!question]- Evento e comando: em que tempo verbal cada um é escrito?
> Evento no **passado** ("Atividade entregue"). Comando no **imperativo** ("Corrigir atividade").

> [!question]- Qual a cor de cada elemento?
> Evento laranja · ponto de atenção rosa (losango) · comando azul · ator amarelo · política roxo claro · modelo de leitura verde claro · sistema externo rosa · pivotal = linha vertical.

> [!question]- O que é um evento pivotal, e por que ele importa?
> Um evento que muda a fase ou o contexto do fluxo. É um forte indicador do limite de um contexto delimitado. → [[Evento de Domínio]]

> [!question]- O que é uma política?
> Uma regra ou automação que, a partir de um evento (com uma condição opcional), dispara um comando sem ator.

> [!question]- Onde fica o modelo de leitura na linha do tempo?
> Antes do comando: é o que o ator consulta para decidir.

## Aula 7 - Levantamento de requisitos
> [!question]- Quais são os 4 riscos de Marty Cagan? Qual vem primeiro e qual é o foco do curso?
> Valor, negócio, usabilidade e técnico. O de **valor** é analisado primeiro. O **técnico** é o foco do curso. → [[Riscos de Produto (Marty Cagan)]]

> [!question]- O que acontece se o dev não participa do upstream?
> Requisito mal compreendido, imprevisibilidade, bugs e débito técnico.

> [!question]- Quais itens o documento da demanda precisa ter?
> Persona, problema e jornada atual, objetivo, jornada da solução e requisitos funcionais e não funcionais.

> [!question]- "99% de disponibilidade" é requisito funcional ou não funcional?
> Não funcional. → [[Requisitos Funcionais e Não Funcionais]]

## Aula 8 - Refinamento técnico
> [!question]- Spike × POC?
> Spike: item dentro da sprint para explorar e aprender. POC: validar se uma solução atende ao objetivo antes de ir para produção. → [[Spike e POC]]

> [!question]- Cite 5 itens do requisito técnico da solução.
> Quaisquer 5 entre: descrição, tecnologias (com justificativa), integrações e dependências, estratégia de implementação, segurança e conformidade, escalabilidade, testes, documentação, plano de implantação (rollout e rollback), critérios de aceitação.

> [!question]- Qual o principal valor do Planning Poker, e qual a limitação dele?
> Provocar a discussão dos impactos no time. Sem base histórica, é pouco assertivo. → [[Estimativas (Planning Poker e Monte Carlo)]]

> [!question]- O que o Monte Carlo responde?
> A probabilidade de o time entregar N itens no período, com base no histórico.

## Aula 9 - DoR e DoD
> [!question]- DoR × DoD?
> DoR: condições para a tarefa **começar**. DoD: critérios para ela estar **concluída**. → [[Definition of Ready e Definition of Done]]

> [!question]- Qual é o DoR do exemplo do curso?
> Requisitos documentados, refinamento técnico, arquitetura desenhada, quebra em itens, estimativa e priorização pelo PM ou PO.

> [!question]- Qual é o DoD do exemplo?
> Code review, aprovação da QA e validação com o usuário final.

## Dúvidas em aberto
- [ ] Os vídeos de Hands On não estão nos PDFs. Vale complementar as notas com o que foi mostrado nas videoaulas (principalmente o mapa de contexto e o Event Storming da escola).

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
