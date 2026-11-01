---
tags: [pos-tech/fase-1, ddd, conceito, design-tatico]
aliases: [Entity, Entidades]
---

# Entidade

Objeto com **identificador único** (nunca reutilizado) e **mutável**: pode e deve ser alterado depois de criado.

- Inserir um item com os mesmos valores de outro **cria uma nova entidade**, porque ela ganha um ID novo.
- Para alterar, localiza-se o item **pelo ID** e muda-se o necessário.

Contraste: [[Objeto de Valor]] (sem ID, imutável, comparado por valor). Entidades e objetos de valor se agrupam em [[Agregado|agregados]].

## Na disciplina Clean Architecture (Fase 2)
- A camada de **Entidades** é a mais interna, no **centro** do diagrama. Guarda os elementos de negócio ("Venda", "Aluno(a)", "Ordem de Pagamento") com os **dados e as regras de consistência** (não existe "Matrícula" sem "Estudante").
- As entidades são definidas **pelos casos de uso** e contêm **só o necessário** (ex.: a Pessoa só precisa do CPF para a Nota Fiscal; o CPF é outra entidade, que se valida).
- Os nomes seguem a **linguagem ubíqua**. Entidades podem especializar ou compor outras.
- **Dois erros**: tratá-las como "classes de dados" inertes, e espelhar a modelagem do repositório de dados ("um-pra-um").
- Detalhes: [[CA 03 - Camada de entidades]] · [[Camadas da Arquitetura Limpa]]

Aparece em: [[DDD 05 - Implementando arquitetura e lógica]], [[CA 02 - Arquitetura Hexagonal e Arquitetura Limpa]], [[CA 03 - Camada de entidades]]
