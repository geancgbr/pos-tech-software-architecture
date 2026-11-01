---
tags: [pos-tech/fase-2, clean-architecture, revisao]
disciplina: Clean Architecture
---

# Revisão - Clean Architecture

[[Clean Architecture]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução e SOLID
> [!question]- A Arquitetura Limpa é uma métrica, certificação ou padrão de projeto?
> Não. É um conjunto de ideias e recomendações para escrever código de melhor qualidade, mais fácil de manter. → [[CA 01 - Introdução e SOLID]]

> [!question]- A Arquitetura Limpa gera menos código?
> Não. Gera mais código, porque é preciso criar unidades que isolem responsabilidades. Também não usa técnicas complicadas: baseia-se em regras de codificação e de arquitetura, e tudo deve ficar explícito.

> [!question]- Por que, sem essa organização, as metodologias ágeis ficam complicadas?
> Porque não é possível aplicar agilidade em código difícil de manter.

> [!question]- Por que se fala em camadas de cebola, e não de bolo?
> Porque, segundo a aula, as camadas são pensadas como grupos de componentes com responsabilidades semelhantes (ex.: na camada de Casos de Uso não pode haver código de conexão com banco). → [[Camadas da Arquitetura Limpa]]

> [!question]- O que diz o princípio da Responsabilidade Única, e qual é a analogia da aula?
> Uma unidade tem uma única responsabilidade e um único motivo para mudar. A analogia é o atendente de lanchonete, que serve de interface padronizada entre cliente e cozinha. → [[SOLID]]

> [!question]- Como aplicar o Aberto-Fechado a um novo formato de relatório?
> Separando o código que gera os dados dos tipos de relatório, em vez de abrir a função existente e colocar mais uma condição.

> [!question]- Qual é a analogia da Segregação de Interface?
> A tomada: o dispositivo não se importa com a instalação elétrica, só com a tensão certa chegando pela mesma interface.

> [!question]- O que diz a Inversão de Dependência?
> Um módulo de alto nível não deve depender de um de baixo nível (segundo a aula, os níveis se referem aos módulos mais perto da infraestrutura). Uma abstração não depende de detalhes: as unidades dependem de abstrações, como interfaces.

> [!question]- Inversão de dependência é o mesmo que injeção de dependência?
> Não. Inversão é passar ao usuário o que ele vai usar sem que ele se importe com como foi criado. Injeção é um dos métodos para fazer isso.

> [!question]- Qual é a diferença de papel entre o SOLID e a Arquitetura Limpa?
> O SOLID indica como cada unidade deve ser construída. A Arquitetura Limpa indica como organizar e pensar a responsabilidade e a interação entre as unidades.

## Aula 2 - Hexagonal e Limpa
> [!question]- A Arquitetura Hexagonal e a Limpa são a mesma coisa?
> Não, mas muitas ideias são semelhantes. A primeira em comum: a camada de Entidades no centro. → [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]]

> [!question]- O que vai na camada de Entidades, além dos dados?
> As regras e restrições de cada elemento, como as de consistência (não existe "Matrícula" sem "Estudante", nem "Venda" sem "Cliente"). → [[Entidade]]

> [!question]- Que linguagem se usa para nomear as entidades?
> A linguagem ubíqua (do DDD): a da regra de negócio e do cliente, não a da implementação.

> [!question]- O que um caso de uso pode usar?
> Só outros casos de uso ou componentes da camada de Entidades. → [[Casos de Uso]]

> [!question]- Input Port × Output Port?
> Input Port informa os dados de que o componente da camada de casos de uso precisa. Output Port define como as respostas são entregues.

> [!question]- Qual é o papel dos Adapters na Hexagonal?
> Adaptar interfaces e dados para a comunicação com um elemento externo (banco, API), isolando-o das camadas internas e convertendo formatos (ex.: do banco para JSON).

> [!question]- Qual é a primeira das diferenças fundamentais da Arquitetura Limpa em relação à Hexagonal?
> As camadas externas aos casos de uso são duas: uma de interface e adaptadores (ligação com o núcleo) e uma mais externa, que implementa as interfaces com o mundo exterior (bancos, APIs).

> [!question]- Quem pode instanciar os elementos das camadas interiores?
> Só os elementos das camadas exteriores.

## Aula 3 - Entidades
> [!question]- Constrói-se primeiro a camada de entidades e depois as outras?
> Não. A criação é integrada, se possível guiada por testes. → [[CA 03 - Camada de entidades]]

> [!question]- No exemplo do mercado, o que é regra de entidade e o que não é?
> De entidade: pagamento não negativo, produto com preço, nenhum pagamento sem ao menos um produto. Não é: um processo de vários passos, como "Efetuar uma Venda".

> [!question]- Quais são os dois cuidados ao criar entidades?
> Não tratá-las como "a camada de classes de dados" (inertes), e não basear as entidades na modelagem do repositório de dados ("um-pra-um").

> [!question]- Por que a Pessoa do exemplo só tem CPF?
> Porque os casos de uso só precisam do CPF (para a Nota Fiscal). Nome, idade e endereço são inúteis nesse contexto. O CPF é outra entidade, que valida o valor.

> [!question]- Por que a regra de pré-requisitos da matrícula não fica na entidade?
> Porque não está ligada diretamente ao estado das entidades: é uma regra complexa, de Caso de Uso. Ela leva, porém, a uma mudança na entidade Estudante (uma lista de disciplinas cursadas).

> [!question]- Em quais dois contextos as entidades são testáveis?
> Na validade dos dados internos e na consistência dos dados dentro de uma regra de negócio.

## Aula 4 - Casos de uso
> [!question]- O que um caso de uso documenta, como ferramenta?
> Um processo de negócio: os dados necessários, os passos, as exceções e como tratá-las, e o resultado. → [[Casos de Uso]]

> [!question]- Por que os cards ágeis costumam se basear em casos de uso?
> Porque com eles se implementa só o necessário, não o desejado.

> [!question]- Um caso de uso pode criar um Estudante a partir de uma Pessoa e matriculá-lo?
> Não. Cada caso de uso faz uma única coisa. Casos complexos se dividem em casos menores, com chamadas explícitas.

> [!question]- Por que, numa classe, os casos de uso são métodos estáticos?
> Porque devem funcionar de forma independente, sem dividir estado.

> [!question]- Quais são as três partes de um caso de uso?
> Os dados que recebe, o algoritmo interno e o retorno.

> [!question]- Por que o caso de uso recebe uma instância do repositório?
> É a Inversão de Dependência: dá para passar um repositório "falso" (mock) e testar a regra. Se funcionar, qualquer erro está no repositório.

> [!question]- O que é um mock?
> Um objeto que se comporta exatamente como a interface pede e retorna os dados para o teste funcionar. Já foi chamado de "fantoche". → [[Mock]]

## Aula 5 - Adaptadores de interface e frameworks e drivers
> [!question]- Os clientes externos podem acessar diretamente os casos de uso?
> Não. Toda requisição é adaptada na recepção e na entrega pela camada de Adaptadores de Interface. → [[Controllers, Presenters e Gateways]]

> [!question]- Controller × Presenter × Gateway?
> Controller: conector que organiza a requisição e chama o caso de uso (um "mensageiro"). Presenter: prepara o retorno no formato do cliente. Gateway: comunicação com componentes externos de dados ou atividades.

> [!question]- Para o Controller existe "sucesso" ou "erro"?
> Não. Ele não sabe como o caso de uso funciona, só como ele recebe e devolve os dados.

> [!question]- Quem normalmente instancia o Presenter?
> O Controller. O Presenter é usado só dentro da camada de Adapters.

> [!question]- Como um Gateway deve expor suas ações?
> Como atividades que o caso de uso entende (ex.: obterEstudatePorPessoa), não como funções de baixo nível do serviço externo.

> [!question]- O que fica na camada Frameworks e Drivers?
> Rotas da API, servidor, tratamento dos dados dos clientes, segurança, autenticação e autorização, interfaces com as origens de dados e, no desktop, telas e botões. Também é chamada de camada de infraestrutura. → [[Detalhes na Arquitetura Limpa]]

> [!question]- Qual é a analogia da camada mais externa?
> A tela, o teclado e as portas de um computador: essenciais para usá-lo, mas fora do funcionamento interno.

## Aula 6 - Componentes
> [!question]- O que significa "responsabilidade bem definida" num componente?
> Fazer coisas simples com total competência (ex.: um componente de banco que faz toda a comunicação), com interfaces de uso explícitas. → [[Componentes de Software]]

> [!question]- A arquitetura monolítica é sempre ruim?
> Não. É adequada para soluções pequenas, com poucas interfaces ou um caso de uso muito específico, como software embarcado. Vira problema quando centraliza muitas responsabilidades e o custo de manutenção cresce. → [[Arquitetura Monolítica]]

> [!question]- O que é a regra da responsabilidade mínima?
> O componente implementa o mínimo possível para ser útil num contexto. O resto vai para outro componente, e nada fica incompleto.

> [!question]- O que é um framework, segundo a aula?
> Uma estrutura de código para agilizar a construção de componentes, como uma casa pré-fabricada. Exemplos: Spring (Java) e Express (JavaScript).

> [!question]- Qual é um dos maiores erros no uso de componentes?
> Adaptar a arquitetura aos componentes ("entortar" a arquitetura para usar componentes familiares), o que gera débito técnico. O certo é desenhar a arquitetura básica primeiro e depois escolher os componentes.

> [!question]- Dois componentes podem compartilhar a mesma responsabilidade?
> Não. Se dois fazem a mesma coisa, como decidir qual usar? Isso não pode existir na Arquitetura Limpa.

## Aula 7 - Detalhes
> [!question]- Por que o mundo exterior é tratado como "detalhe"?
> Não porque seja sem importância, mas porque o software não depende dele e funciona independentemente desses recursos. → [[Detalhes na Arquitetura Limpa]]

> [!question]- Quais são as duas características da Arquitetura Limpa destacadas na aula 7?
> O isolamento do contexto de regra de negócio em relação ao contexto de execução, e a independência do software em relação ao contexto de execução.

> [!question]- Por que "repositórios de dados" e não "bancos de dados"?
> Porque hoje há várias soluções que servem de origem e destino de dados, inclusive APIs externas.

> [!question]- O que é Backend for Frontend?
> Criar um grupo de APIs (backend) para cada tipo de cliente (frontend), deixando a adaptação na camada mais externa. → [[Backend for Frontend (BFF)]]

> [!question]- Quais são as duas abordagens para usar frameworks na Arquitetura Limpa?
> Usar micro-frameworks, ou usar um framework robusto a favor da estrutura (ex.: ORM isolado como Gateway; casos de uso numa biblioteca separada dos Controllers).

## Aula 8 - Revisão
> [!question]- Quais são as 4 camadas, de dentro para fora?
> Entidades, Casos de Uso, Adaptadores de Interface e Frameworks e Drivers. → [[CA 08 - Revisão da disciplina]]

> [!question]- Quais são as duas regras de interação entre componentes?
> 1) Os internos não dependem nem acessam diretamente os externos; recebem-nos por injeção de dependência, via uma interface que definem. 2) Componentes da mesma camada podem interagir e depender entre si.

> [!question]- Quais componentes a aula 8 lista nos Adaptadores de Interface?
> Controllers, Gateways e Adapters. Atenção: a aula 5 lista Presenters no lugar de Adapters.

> [!question]- Como a Arquitetura Limpa vê os recursos externos?
> Como serviços externos, não como dependências: são detalhes.

## Dúvidas em aberto
- [ ] **Presenters × Adapters** (aula 5 × aula 8): ver qual nome o professor usa na prova.
- [ ] **"O que" × "como"** dos casos de uso (aula 4): ver qual formulação vale.
- [ ] O código das aulas 3 e 4 (Pessoa/CPF, registro de Estudante) está em imagem nos PDFs. Os Hands On das aulas 3, 4, 5, 7 e 8 trazem links de bases de dados para treinar o conteúdo.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
