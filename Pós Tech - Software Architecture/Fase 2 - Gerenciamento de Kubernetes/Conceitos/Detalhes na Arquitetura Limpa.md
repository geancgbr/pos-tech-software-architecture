---
tags: [pos-tech/fase-2, clean-architecture, conceito]
aliases: [Detalhes, Mundo exterior como detalhe, Repositórios de dados, Frameworks e Drivers]
---

# Detalhes na Arquitetura Limpa

Repositórios de dados, modo de acesso e tudo o que se relaciona com o mundo exterior são tratados como **"detalhes"**: são importantes, mas o software **não depende** deles. Tratar o mundo exterior como detalhe é um dos principais responsáveis por a Arquitetura Limpa **conseguir** isolar as regras de negócio.

**Duas características**: isolamento do contexto de negócio (o **"quê"**) em relação ao de execução (o **"como"**) · independência do contexto de execução (repositório, tipo de API, framework).

| Detalhe | Como tratar |
|---|---|
| **Repositórios de dados** | São serviços fora do escopo do software (bancos de vários tipos, APIs externas). Componentes na camada mais externa e **Gateways** padronizando a comunicação. "A origem é apenas um detalhe" |
| **Acesso à aplicação** | Vários clientes (mobile, navegador, desktop, clientes futuros), por Web API, socket, cliente nativo ou eventos. Acesso isolado em componentes; internamente, só as requisições dos **Controllers** importam. Exemplo: [[Backend for Frontend (BFF)]] |
| **Frameworks** | **Micro-frameworks**, ou um framework robusto **a favor da estrutura** (ex.: ORM isolado como Gateway; casos de uso numa biblioteca separada dos Controllers) |

**A camada Frameworks e Drivers** (aula 5): a mais externa, também chamada de **camada de infraestrutura**. Tem rotas, servidor, autenticação e autorização, telas, conexões e o controle de erros dos serviços externos. Na analogia do computador, é o teclado, a tela e as portas.

Aparece em: [[CA 05 - Adaptadores de interface e frameworks e drivers]], [[CA 07 - Detalhes - dados, acesso e frameworks]], [[CA 08 - Revisão da disciplina]]
