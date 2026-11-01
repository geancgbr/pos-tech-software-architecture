---
tags: [pos-tech/fase-1, arquitetura, revisao]
disciplina: Arquitetura de Software
---

# Revisão - Arquitetura de Software

[[Arquitetura de Software]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- Como a apostila define arquitetura de software?
> Estrutura lógica e física de um sistema, incluindo componentes, suas interações e suas restrições de design. Determina como o sistema deve ser construído e como os componentes se integram. → [[O que é Arquitetura de Software]]

> [!question]- Em quais qualidades a arquitetura interfere?
> Flexibilidade, escalabilidade, desempenho e segurança.

> [!question]- Quais fatores considerar ao criar uma arquitetura?
> Requisitos de negócio, restrições de tempo e orçamento, padrões de design e tecnologias.

> [!question]- Quais são as três abordagens de arquitetura citadas?
> Baseada em camadas, em componentes e em serviços.

> [!question]- Quais são os principais pontos do livro Clean Architecture?
> Separação de preocupações, responsabilidade única, abstração, depuração fácil e simplicidade. Autor: Robert C. Martin ("Uncle Bob"). → [[Clean Architecture (livro)]]

> [!question]- Quais são as 3 categorias de design patterns?
> Criação, estruturais e de comportamento. → [[Design Patterns]]

> [!question]- Cite os 4 padrões de criação.
> Factory, Builder, Singleton e Prototype.

> [!question]- Qual padrão garante uma única instância com acesso global?
> Singleton.

> [!question]- Quais são as subcategorias dos padrões estruturais, e quais padrões há em cada uma?
> Adaptação: Adapter, Bridge, Proxy. Agregação: Composite, Decorator, Façade. Composição: Flyweight, Private Class Data, Bridge.

> [!question]- Quais são as subcategorias dos padrões de comportamento, e quais padrões há em cada uma?
> Classe: Template Method, Strategy, State. Objeto: Observer, Chain of Responsibility, Command. Interação: Interpreter, Mediator, Visitor.

> [!question]- Qual padrão define uma dependência um-para-muitos com notificação automática?
> Observer.

> [!question]- Qual padrão encapsula a solicitação como objeto e suporta desfazer e refazer?
> Command.

> [!question]- Quais são as camadas mais comuns na arquitetura de camadas, e qual delas tem a lógica de negócios?
> Apresentação/interface do usuário, aplicação e persistência de dados. A lógica de negócios fica na **aplicação**. → [[Arquitetura de Camadas]]

> [!question]- Na pilha de camadas, quem fornece serviços para quem?
> As camadas mais baixas fornecem serviços para as mais altas.

## Aula 2 - Processo e modularização
> [!question]- Quais são as etapas do processo de desenvolvimento de software?
> Análise de requisitos, design, implementação, testes e manutenção. → [[Processo de Desenvolvimento de Software]]

> [!question]- Para quem trabalha com DDD, a que corresponde a etapa de levantamento de requisitos?
> À modelagem tática: entrevistar clientes e stakeholders. → [[Modelagem Tática]]

> [!question]- O que muitos analistas deixam de registrar, e por que isso faz falta?
> A linguagem ubíqua. Ela ajuda no decorrer do desenvolvimento, quando é preciso voltar a conversar com os stakeholders.

> [!question]- O que é modelagem tática, segundo esta disciplina?
> Análise e planejamento que define ações específicas para objetivos operacionais e estratégicos, com planos detalhados para metas de curto e médio prazo.

> [!question]- O que é linguagem ubíqua, segundo esta disciplina?
> Linguagem comum, clara e consistente, entendida por todos os envolvidos (desenvolvedores, usuários, clientes, partes interessadas). Também chamada de linguagem onipresente. → [[Linguagem Ubíqua]]

> [!question]- O que é modularização, e quais são as vantagens dela?
> Dividir o sistema em módulos independentes, com funções específicas, desenvolvidos, testados e mantidos separadamente. Vantagens: mais fácil de entender, modificar e atualizar; mais flexível; erros detectados por módulo; equipes em paralelo. → [[Modularização]]

> [!question]- Que cuidado a modularização exige?
> Interfaces entre módulos claras e bem definidas, e organização lógica e coerente.

> [!question]- Quais foram os módulos da nova versão do REC?
> Usuários (com gerenciamento de perfil), Canais (com gerenciamento) e Redes sociais (compartilhamento de conteúdo).

## Aula 3 - Documentação, testabilidade e modificabilidade
> [!question]- Quais são os 4 tipos de documentação citados?
> Utilização do projeto, desenvolvimento do projeto, infraestrutura e arquitetura do projeto. → [[Documentação de Software]]

> [!question]- Um manual do usuário é que tipo de documentação?
> Documentação de utilização do projeto.

> [!question]- Um relatório de testes é que tipo de documentação?
> Documentação de desenvolvimento do projeto.

> [!question]- Cite itens da documentação de infraestrutura.
> Inventário de hardware, inventário de software, diagramas de rede, políticas e procedimentos, documentação de configuração e relatórios de monitoramento.

> [!question]- Cite itens da documentação de arquitetura do projeto.
> Visão geral, diagramas de arquitetura, padrões de design, descrição dos componentes, interfaces do sistema e decisões de design.

> [!question]- Quais ferramentas de documentação foram mostradas no Hands On?
> Swagger e Redoc.

> [!question]- O que é testabilidade, e quais fatores a afetam?
> A capacidade de o software ser testado de maneira eficaz. Fatores: design, arquitetura, instrumentação de código, dados de teste, ferramentas de teste e acessibilidade de interfaces. → [[Testabilidade]]

> [!question]- O que é instrumentação de código?
> Adicionar código para coletar dados para análise, monitoramento e teste.

> [!question]- O que é modificabilidade, e quais fatores a afetam?
> A capacidade de o software ser modificado facilmente. Fatores: design, arquitetura, qualidade do código, documentação e testabilidade. → [[Modificabilidade]]

> [!question]- Testabilidade e modificabilidade devem ser tratadas como requisitos?
> Sim. As duas devem ser consideradas requisitos importantes. A testabilidade, especificamente, não deve ser tratada como um processo secundário ou opcional.

## Aula 4 - Escalabilidade, disponibilidade e desempenho
> [!question]- O que é escalabilidade?
> A capacidade de crescer e se adaptar a um aumento de demanda (usuários, dados, tráfego) sem prejudicar o desempenho ou a confiabilidade. → [[Escalabilidade]]

> [!question]- Quais são as 4 estratégias de escalabilidade?
> Arquitetura escalável (sistemas distribuídos, balanceamento de carga), tecnologias modernas (nuvem, contêineres), banco de dados escalável (NoSQL, cache) e monitoramento e otimização.

> [!question]- Quais ferramentas de monitoramento a apostila cita?
> New Relic, Nagios, Splunk, AppDynamics e VisualVM.

> [!question]- Qual delas é de código aberto e voltada a aplicativos Java?
> VisualVM.

> [!question]- O que foi mostrado no Hands On?
> Health check, Zabbix (notificações), Prometheus e Grafana com Docker, e Azure Container Apps (PaaS para Kubernetes) para escalar.

> [!question]- Disponibilidade × observabilidade: definição e medida de cada uma?
> Disponibilidade: estar disponível para uso quando necessário, medida em tempo de atividade em relação ao tempo total. Observabilidade: observar e medir o comportamento em tempo real, medida por métricas de desempenho (tempo de resposta, taxa de erros, utilização de recursos). São complementares. → [[Disponibilidade e Observabilidade]]

> [!question]- Quais são as dimensões do desempenho?
> Tempo de resposta, taxa de transferência, utilização de recursos, confiabilidade e escalabilidade. → [[Desempenho]]

> [!question]- O que é cache, e quais estratégias a apostila cita?
> Armazenar temporariamente em memória os dados acessados com frequência, para não buscá-los de novo na origem. Estratégias: página inteira, banco de dados, objeto, sessão e CDN. → [[Estratégias de Cache]]

> [!question]- Em qual estratégia de cache a apostila cita os dados do carrinho de compras?
> No cache de sessão, junto com preferências e histórico de navegação.

## Aula 5 - Arquitetura Hexagonal
> [!question]- Quem propôs a arquitetura hexagonal, quando, e com que princípio?
> Alistair Cockburn, em meados dos anos 1990 (artigo na WikiWikiWeb), com base no princípio de Separação de Conceitos (SoC). → [[Arquitetura Hexagonal]]

> [!question]- O que é SoC, e qual exemplo a apostila usa?
> Modularizar a solução para que cada módulo resolva um único problema. Exemplo: o MVC (View apresenta, Model trata as regras de negócio, Controller faz o intermédio). → [[Separação de Conceitos (SoC)]]

> [!question]- Quais são as 3 áreas da arquitetura hexagonal?
> O centro do hexágono, o lado (superior) esquerdo e o lado (inferior) direito, fora do hexágono.

> [!question]- Quais são os objetivos da arquitetura hexagonal?
> Reusabilidade de código, alta coesão, baixo acoplamento, independência de tecnologia e facilidade de teste (objetivos parecidos com os da arquitetura limpa).

> [!question]- O nome "hexagonal" tem relação com o número 6?
> Não. A referência é ao polígono, com vários lados que representam as diferentes implementações e tecnologias. Poderia ser um pentágono ou um heptágono.

> [!question]- Qual outro nome Cockburn tentou dar à arquitetura, e quando?
> Arquitetura Baseada em Portas e Adaptadores, em 2005.

> [!question]- O "Application" do centro do hexágono é a camada de aplicação da arquitetura de camadas?
> Não, não tem relação. É o core, a camada de domínio, o coração do sistema.

> [!question]- O centro do hexágono pode depender de algum framework?
> Deve ser agnóstico a tecnologia, framework e infraestrutura, mas pode depender de frameworks de serviços gerais, como log e IoC.

> [!question]- O que é uma porta, e onde ela fica?
> Um conceito lógico que define um ponto de entrada e saída: uma interface de programação. Fica no centro do hexágono, porque é independente de tecnologia. → [[Portas e Adaptadores]]

> [!question]- Porta de entrada × porta de saída?
> Entrada: de fora para dentro, declara os serviços **providos** pelo sistema. Saída: de dentro para fora, declara os serviços **requeridos** (por exemplo, o banco de dados). Fonte: Marco Tulio Valente.

> [!question]- Qual a função de um adaptador, e quantos deve haver por porta?
> Implementar a conexão entre uma porta e os serviços externos. Pelo menos dois por porta: um para teste e um para a implementação real (por exemplo, Redis e cache em memória).

> [!question]- Ator condutor × ator conduzido?
> Condutor (lado esquerdo): recebe chamadas de fora e as encaminha às portas de entrada (HTTP, testes, mobile, web, CMD). Conduzido (lado inferior direito): recebe chamadas dos casos de uso e as direciona a sistemas externos, acionado pelas portas secundárias (banco, SMTP). → [[Atores Condutores e Conduzidos]]

> [!question]- Quais são os tipos de ator conduzido?
> Repositório (envia e recebe; por exemplo, banco de dados) e Destinatário (envia e esquece; por exemplo, SMTP).

> [!question]- Quais são os 5 passos do fluxo de execução?
> 1) Um adaptador externo recebe e adapta a solicitação. 2) O adaptador envia para uma porta. 3) A porta executa a lógica de negócio com entidades e serviços. 4) A porta envia a resposta para outro adaptador, que a adapta. 5) O adaptador devolve a resposta à interface, que a apresenta ao usuário.

> [!question]- Que problema aparece no fluxo, e como Cockburn o resolveu?
> O centro do hexágono passa a depender do lado direito (atores conduzidos). Ele resolveu com Inversão de Controle (IoC). → [[Inversão de Controle (IoC)]]

> [!question]- O que é IoC?
> Um princípio em que a sequência de chamadas de métodos é invertida e não é determinada diretamente pelo programador. O controle é delegado a uma infraestrutura de software, muitas vezes chamada de contêiner, ou a outro componente que possa tomar o controle da execução. É um padrão utilizado em projetos orientados a objetos, que utilizam interface, herança e polimorfismo.

## Dúvidas em aberto
- [ ] Os vídeos de Hands On não estão nos PDFs. Vale complementar com o que foi mostrado nas videoaulas (REC, Swagger e Redoc, BDD, Prometheus e Grafana, código da hexagonal).

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
