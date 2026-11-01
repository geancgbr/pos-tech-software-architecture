---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 3
fonte: "Aula 3.pdf (Erick Muller)"
---

# CA 03 - Camada de entidades

← [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]] · [[Clean Architecture]] · Próxima → [[CA 04 - Camada de casos de uso]]

> [!summary] Em uma frase
> As [[Entidade|entidades]] são a camada **mais interna**: os elementos que a regra de negócio usa (pessoa, disciplina, venda, produto), com seus dados e **regras de validação**. São definidas **pelos casos de uso**, contêm só o necessário e **não espelham o repositório de dados**.

## Hands On
O que é a camada de entidades, para que serve e como criar entidades, com exemplos e regras da Arquitetura Limpa. O PDF traz um link para uma base de dados no GitHub, para treinar.

## Como pensar as entidades
- A Clean Architecture mantém **independência** entre as responsabilidades da regra de negócio e as da interação com o mundo exterior. As camadas internas (Casos de Uso e Entidades) tratam do **"o que"** o software faz.
- **Não se define primeiro a camada de entidades e depois as outras**: o software é construído de forma **integrada**, se possível **guiado por testes**, pensando sempre em camadas e responsabilidades.
- Na análise, os requisitos viram **Casos de Uso**, que documentam o que o software faz a cada interação com um **agente externo** (pessoa, outro software...). Para detalhar o caso de uso, importa menos quem é o agente e mais o que ele precisa fazer, que resposta espera e qual é o resultado.

> [!example] Exemplo do mercado
> "Uma pessoa entra no mercado, pega um produto, leva ao caixa, onde é gerada uma compra com valor total, faz o pagamento e leva o produto."
> **Entidades**: pessoa, mercado, produto, caixa, pagamento.
> **Regras das entidades**: o pagamento não pode ser negativo; o produto precisa ter preço; não há pagamento sem ao menos um produto na compra.
> Essas regras são dos **elementos e dos relacionamentos**. Um processo de vários passos, como "Efetuar uma Venda", **não** é regra de entidade.

- Uma entidade pode **especializar** outra, ser **composta** de outras ou ser definida em si mesma.
- **Nomes**: pela [[Linguagem Ubíqua|linguagem ubíqua]] do DDD, os mesmos que as pessoas do domínio usam. Nomes incomuns levam a entidades desconectadas da realidade.
- **Implementação**: classes, tipos ou structs, conforme a linguagem. Cada elemento se diferencia pelas **características, ações e estados internos**.

## Os dois cuidados
| Erro | Por que é ruim |
|---|---|
| Tratar as entidades como **"a camada de classes de dados"** | Cria classes inertes, que só armazenam e validam dados. É preciso pensar no **papel** de cada entidade na estrutura. Sem isso, perde-se um dos objetivos da Arquitetura Limpa: identificar responsabilidades em cada camada |
| Basear as entidades na **modelagem do repositório de dados** (conexão direta "um-pra-um" entre as entidades do repositório e as classes de entidades, comum em frameworks) | Erro **estrutural**: a entidade espelha os tipos de dados da implementação externa, herda nomes sem significado e pode terceirizar validações para o repositório. A Arquitetura Limpa fica **impossível** onde esse acoplamento é obrigatório, ou onde o software só serve de interface para um banco |

## Exemplo da aula: Pessoa e CPF
O código está na Figura 1 do PDF. O que o texto descreve:
- Para os casos de uso, a **Pessoa** só precisa do **CPF** (para a Nota Fiscal). Por isso nome, idade e endereço **não entram**: são inúteis nesse contexto.
- O **CPF** vira outra entidade, que valida o valor. Se o CPF for inválido, a criação da Pessoa retorna erro.
- **Lições**: implemente na entidade só o necessário, e implemente junto com ela as regras de validação que a tornam consistente.

## Entidades e casos de uso
- As entidades **não são definidas por si**, e sim **no contexto dos casos de uso**. Não se cria uma entidade porque se acha que ela é necessária, e sim de acordo com o que é necessário. Bem implementada, ela é a **abstração de um ator** do caso de uso.
- **Testáveis em dois contextos**: a validade dos dados internos e a consistência dos dados dentro de uma regra de negócio.

> [!example] Exemplo: matrícula
> Estudante (nome, idade, endereço) e Disciplina (nome, oferta atual) podem ser criados e testados isoladamente.
> Mas a regra "para se matricular, precisa ter os pré-requisitos e não pode ter sido aprovado nessa disciplina" é uma **regra complexa de Caso de Uso**, não das entidades.
> Essa regra leva a uma **mudança na entidade**: o Estudante passa a ter uma **lista de disciplinas já cursadas**.

**Os casos de uso orientam as alterações nas entidades.**

## Resumo da própria apostila
As entidades representam os dados manipulados pela regra de negócio e suas responsabilidades. Definem o que os casos de uso manipulam, as regras internas, a validade do estado, como se comunicam e os limites de responsabilidade. **Não se relacionam com as entidades do repositório de dados** e contêm só o necessário para os casos de uso funcionarem.

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008)
