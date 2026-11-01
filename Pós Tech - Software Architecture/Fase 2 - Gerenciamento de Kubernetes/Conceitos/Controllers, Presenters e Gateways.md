---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Controller, Controllers, Presenter, Presenters, Gateway, Gateways, Adaptadores de Interface, Interface Adapters]
---

# Controllers, Presenters e Gateways

Os componentes da camada de **Adaptadores de Interface**, que intermedeia o mundo externo e os casos de uso. Os clientes **nunca acessam os casos de uso diretamente**: tudo é adaptado na entrada e na saída.

| Componente | Papel |
|---|---|
| **Controller** | **Conector** entre as camadas: recebe a requisição, transforma os dados em entidades, chama o caso de uso e prepara o retorno. Não sabe como o caso de uso funciona; para ele não existe "sucesso" ou "erro". É um **"mensageiro"** |
| **Presenter** | Prepara os **dados de retorno** no formato que o cliente entende (ex.: padrões HTTP, cabeçalhos, Content). Normalmente é instanciado pelo Controller e usado só dentro da camada |
| **Gateway** | Comunicação com **componentes externos** de dados ou atividades (ex.: repositórios). Expõe **ações como atividades** (`obterEstudatePorPessoa`), não funções de baixo nível. Os casos de uso o recebem por **injeção de dependência** |

> [!warning] Na aula 8, a lista é Controllers, **Gateways e Adapters**
> O "Adapter" da aula 8 faz o que a aula 5 chama de **Presenter**: é usado pelos Controllers para adaptar o formato do retorno.

**Analogias da aula 5**: o balconista de lanchonete (cardápio padrão) e o vendedor de loja de roupas (entende e adapta à necessidade).

Aparece em: [[CA 05 - Adaptadores de interface e frameworks e drivers]], [[CA 07 - Detalhes - dados, acesso e frameworks]], [[CA 08 - Revisão da disciplina]]
