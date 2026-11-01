---
tags: [pos-tech/fase-2, conceito, testes]
aliases: [Mocks, Mock object, Mock objects, Fantoche]
---

# Mock

**Clean Architecture (aula 4)**: um objeto que **se comporta exatamente como a interface pede** e retorna os dados necessários para o teste funcionar. Não tem correspondente em português; já se usou **"fantoche"**, um objeto que "se comporta como" um real, mas manipulado para um propósito específico.
- Uso: testar um caso de uso com um **repositório mock**, antes de conectar as interfaces externas. Se a regra funciona, qualquer erro está no repositório, não no código.
- Isso é possível pela **inversão de dependência** ([[SOLID]]).

**Qualidade de Software (Fase 1)**: no teste de integração **Bottom-Up**, as dependências externas são simuladas, ou se usam **mock objects** ([[Teste de Integração]]). O resumo da aula 2 de Qualidade cita "maneiras para criar mock", sem detalhar.

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
No Hands On, **mocks** simulam as dependências do `CatalogoService` nos testes unitários; segundo o resumo, **mocks e stubs** diminuem a complexidade e focam os testes na funcionalidade alvo ([[MS2 03 - Testando microsserviços]]).

Aparece em: [[CA 04 - Camada de casos de uso]], [[QS 04 - Testes de integração]], [[MS2 03 - Testando microsserviços]]
