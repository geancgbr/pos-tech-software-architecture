---
tags: [pos-tech/fase-2, devops, aula]
disciplina: DevOps (IaC and CI/CD)
aula: 3
fonte: "Aula 3 - DevOps - Testes Automatizados com CI_revFinal.pdf (Fabiano da Silva Carneiro)"
---

# DEV 03 - Testes automatizados com CI

← [[DEV 02 - Melhores práticas com o GitHub]] · [[DevOps (IaC and CI-CD)]] · Próxima → [[DEV 04 - Qualidade do código-fonte]]

> [!summary] Em uma frase
> No DevOps, o teste cobre **todo o ciclo de vida** e é **automatizado e contínuo**: roda num pipeline a cada alteração do código, e o processo **não continua se houver erro**. Teste automático e **[[Testes Contínuos|teste contínuo]]** não são a mesma coisa.

## Hands On (vídeo)
Testes do ponto de vista do DevOps, como colocá-los na esteira de CI e em diferentes metodologias ágeis. Na prática, com o **GitHub Actions**: **testes unitários, smoke test, teste de integração e testes funcionais**. O PDF traz o link "Códigos da aula 3".

## Testes no DevOps
- O DevOps leva o modelo ágil **um passo adiante**, aproximando o lançamento e a implantação do desenvolvimento e do teste. **Uma equipe ágil responde, sozinha, pelo desenvolvimento, teste e lançamento** do que cria.
- Os testadores não se concentram mais só em testes funcionais e de features. Também fazem **testes de operações, de desempenho, testes básicos de segurança** e **monitoram e analisam dados e registros de produção**.
- **O teste é automatizado e contínuo**, executado por um **workflow automatizado (pipeline)**.

## Testes na integração contínua
- A CI não é só entregar continuamente com controle de código, mas **aumentar a qualidade**: entregas rápidas, verificações constantes, bugs encontrados antes, menos tempo de teste nas equipes de validação e menos tempo para novas versões.
- **Valores da CI** (Glover, Duvall e Matyas): diminuir riscos · reduzir processos manuais repetitivos · gerar software a qualquer momento e em qualquer lugar · maior visibilidade do projeto · maior confiabilidade no produto.
- **Para diminuir riscos, reduzir processos manuais e ter mais confiabilidade, são necessários testes.**
- A CI precisa de testes executados **constantemente**, para evitar erros simples, verificar o funcionamento básico, **impedir que erros já corrigidos voltem** e garantir que a qualidade da versão nova seja **no mínimo igual à anterior**.
- A CI deve ser **totalmente automatizada**, aumentando a cobertura de testes a cada versão.

## TDD: o único processo manual
- Tudo começa quando o dev cria um teste que **falha em 100% das tentativas**. Aos poucos, ele escreve o código e reescreve o teste até o código ficar pronto. Isso é o **TDD** (Test Driven Development), mostrado na Figura 2 do PDF.
- É **o único processo totalmente manual**, e de extrema necessidade. Ou seja, **a integração contínua começa com um teste manual**.
- Sem automação de testes, a empresa pode criar um **documento interno** com a sequência de testes a executar, mas esse **não é um cenário aconselhável** hoje. Pela CI (Glover, Duvall e Matyas), é preciso diminuir os processos manuais, e o teste é um deles.

Veja [[TDD (Test-Driven Development)]].

## Teste automático × teste contínuo
- A CI vem do **Extreme Programming**, criado **no mínimo 10 anos antes do DevOps**, que já previa testes automáticos. O que muda no DevOps?

| Teste automático | Teste contínuo |
|---|---|
| Executado por **estímulo humano** (comandos no computador, IDE) | Executado **automática e continuamente** a cada alteração no repositório, num **workflow**: se passar, segue para a próxima etapa |

- **A base são os testes "técnicos"**: integração, componentes e unitários.
- No modelo tradicional, com a homologação quase toda manual, não há como garantir que os testes técnicos foram executados.
- **Os testes técnicos são 90% de todos os testes que deveriam ser executados** (Figura 3), principalmente porque um erro encontrado nessa fase tem **custo, esforço e tempo menores** do que nas fases seguintes.

## Pipeline de testes
- **Benefício**: mesmo que o dev não rode os testes, **o pipeline obrigatoriamente roda**. Mas a automação deve executar **os mesmos "comandos" que o dev**, principalmente no teste unitário.

| Linguagem | Build/Teste |
|---|---|
| Java (ant) | Ant build |
| Java (maven) | `mvn test` / `mvn verify` |
| .NET | `dotnet test` |
| Node | `npm test` |
| Python | `pytest` |

**Exemplo com Java Maven**
```yaml
steps:
  - uses: actions/checkout@v3
  - uses: actions/setup-java@v3
    with:
      java-version: '17'
      distribution: 'temurin'
  - name: Run the Maven verify phase
    run: mvn --batch-mode --update-snapshots verify
```

**Exemplo com Node.js**
```yaml
name: Node.js CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '12.x'
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
```

**A boa estratégia é testar tudo o que for possível**, dos testes unitários (mais ligados à CI) até os **funcionais em homologação e produção** (Figuras 4 e 5).

## Referência
Duvall, Matyas e Glover, *Continuous Integration* (2007)
