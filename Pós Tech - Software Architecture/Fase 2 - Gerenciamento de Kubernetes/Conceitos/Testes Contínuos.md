---
tags: [pos-tech/fase-2, devops, conceito, testes]
aliases: [Teste contínuo, Testes automatizados com CI, Pipeline de testes, Teste automático]
---

# Testes Contínuos

| Teste automático | Teste contínuo |
|---|---|
| Executado por **estímulo humano** (comando, IDE) | Executado **automaticamente a cada alteração** no repositório, dentro de um workflow: se passar, segue para a próxima etapa |

- **A base são os testes técnicos** (integração, componentes, unitários): **90%** dos testes que deveriam ser executados, porque um erro encontrado cedo custa menos.
- **A CI começa com um teste manual**: o **TDD** é o único processo totalmente manual ([[TDD (Test-Driven Development)]]).
- **Pipeline**: roda os testes **obrigatoriamente**, com **os mesmos comandos do dev** (`mvn test`/`mvn verify`, `dotnet test`, `npm test`, `pytest`, Ant build).
- **Estratégia**: testar tudo o que for possível, do unitário (CI) ao funcional (homologação e produção).
- **No Hands On** (GitHub Actions): unitários, **smoke test**, integração e funcionais.

Na Fase 1: [[Testes de Software]], [[Teste de Unidade]], [[Teste de Integração]].

Aparece em: [[DEV 03 - Testes automatizados com CI]]
