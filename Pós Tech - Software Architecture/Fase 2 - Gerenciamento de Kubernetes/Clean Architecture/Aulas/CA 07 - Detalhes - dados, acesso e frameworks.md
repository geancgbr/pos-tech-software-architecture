---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 7
fonte: "Aula 7.pdf (Erick Muller)"
---

# CA 07 - Detalhes: dados, acesso e frameworks

← [[CA 06 - Componentes]] · [[Clean Architecture]] · Próxima → [[CA 08 - Revisão da disciplina]]

> [!summary] Em uma frase
> Na Arquitetura Limpa, o mundo exterior (repositórios de dados, modo de acesso e tudo o que se relaciona com ele) é tratado como **"detalhe"**. Isso não quer dizer que não importe, e sim que o software **não depende** dele. Veja [[Detalhes na Arquitetura Limpa]].

## Hands On
Como tomar boas decisões de arquitetura diante das restrições de alguns detalhes, e como equilibrar a realidade com o desenho. O PDF traz um link para uma base de dados da aula.

## Duas características da Arquitetura Limpa
1. **Isolamento do contexto de regra de negócio do contexto de execução**: os componentes das regras de negócio, que entregam as funcionalidades (o **"quê"**), ficam separados dos que falam com o ambiente de execução (o **"como"**).
2. **Independência em relação ao contexto de execução**: o software não depende de um tipo específico de repositório de dados, de arquitetura de comunicação (como uma API web) ou de framework. **As funcionalidades não são estruturadas de acordo com um framework.**

Antes, o desenho era um **monólito**, com as regras de negócio espalhadas pelos componentes e até servindo de integração entre eles (Figura 1 do PDF). Na Arquitetura Limpa, os **componentes ficam isolados** (Figura 2).

## A mudança na estrutura das arquiteturas
| | Antes, pré-internet (Figura 3) | Hoje (Figura 4) |
|---|---|---|
| Ambiente | **Homogêneo**: dentro da empresa, com recursos conhecidos | **Heterogêneo**: dispositivos e ambientes desconhecidos, mas com padrões (Android, iOS, navegadores) |
| Dados | Um único banco de dados | Vários serviços e repositórios |
| Rede e clientes | Rede isolada, computadores conhecidos, software nativo instalado | Acesso de qualquer dispositivo; infraestrutura em nuvem e baseada em serviços |
| Integração | Quase inexistente, e quando havia era desconectada e assíncrona | Componentes conectados a vários serviços |

Até grandes empresas tinham data centers internos e conexões precárias entre filiais. **O desafio hoje** é resolver problemas nesse contexto heterogêneo.

## Os repositórios de dados
- Os dados ficam num recurso **fora do escopo do software**, usado **como serviço**. Por isso se fala em **"repositórios de dados"**, não só "bancos de dados":
  - uma **API externa** pode ser uma origem de dados válida, isolada como componente de acesso a dados;
  - há **várias tecnologias de banco**, escolhidas por desempenho e tipo de armazenamento.
- Para as camadas internas, **não importa a origem nem o destino**, só que funcionem. Os componentes de comunicação ficam na **camada mais externa**, e os **Gateways** padronizam a comunicação. **A origem é apenas um detalhe.**

## O acesso à aplicação
- O software deve atender **vários clientes** (mobile, navegador, desktop) e estar pronto para clientes **não previstos**.
- Normalmente o acesso é por **API**, e a mais famosa é a **Web API (HTTP)**. Também existem **socket**, **cliente nativo** e **comunicação por eventos**.
- **O problema do acoplamento**: se as regras de negócio, ou o controle de execução, estiverem acopladas a uma forma de acesso, o software só pode ser acessado de **uma maneira**. Ou cada cliente cria software extra para se adaptar, ou é preciso reescrever a comunicação, muitas vezes **duplicando a regra de negócio**.
- **Solução**: isolar o acesso em um ou mais componentes. Internamente, só se trabalha com as requisições dos **Controllers**. **Como a comunicação funciona é apenas um detalhe.**

## Exemplo: Backend for Frontend (BFF)
Um **grupo de APIs (backend) para cada cliente (frontend)**. Com um endpoint único para mobile e desktop, o código da funcionalidade teria de descobrir o tipo de chamada e o formato do retorno. Com um endpoint por cliente, essa responsabilidade fica na **camada mais externa**:

```javascript
app.get('/mobile/products', (_req, _res) => {
  const pc = new ProductsController();
  const all_products = pc.getAllWithFields(['name', 'identifier']);
  return JSON.stringify(all_products);
})

app.get('/browser/products', (_req, _res) => {
  const pc = new ProductsController();
  const all_products = pc.getAll();
  return JSON.stringify(all_products);
})
```
Assim o Controller não precisa de regra de negócio para decidir como atender cada cliente. Veja [[Backend for Frontend (BFF)]].

## Frameworks
Frameworks **full-stack** ou **micro-frameworks** especializados agilizam a entrega com qualidade. Mas muitos têm componentes integrados. Como manter o isolamento?
1. **Micro-frameworks**: cada componente continua com uma única tarefa e baixo acoplamento.
2. **Framework mais robusto, usado a favor da estrutura**: usar as ferramentas do framework sem basear o código no que ele indica. Dá mais trabalho, mas mantém as camadas. Exemplos:
   - isolar o **ORM** numa camada de acesso a dados, usada como **Gateway** dentro dos Controllers;
   - isolar os **casos de uso** dos Controllers numa **biblioteca** dentro do software.

## Resumo da própria apostila
Não dá para entregar software de qualidade sem recursos externos, mas isso não exige **depender diretamente e fortemente** deles. Pensando neles como **detalhes**, a arquitetura fica robusta e **à prova de alterações** nos recursos que usa.

## Referências
Evans, *Domain-Driven Design* (2003) · Fowler, *UseCase* · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008)
