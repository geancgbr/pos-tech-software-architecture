---
tags: [pos-tech/fase-1, qualidade, revisao]
disciplina: Qualidade de Software
---

# Revisão - Qualidade de Software

[[Qualidade de Software]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Principais conceitos
> [!question]- Qual é a finalidade dos testes de software?
> Descobrir erros de programação, falhas de lógica, comportamentos inesperados e vulnerabilidades de segurança, identificando e corrigindo defeitos antes do lançamento. → [[Testes de Software]]

> [!question]- Por que as empresas destroem carros, foguetes e equipamentos para testar?
> Porque a confiança é crucial: o usuário precisa confiar que o produto funciona e que seus dados estão seguros. Testes rigorosos mostram compromisso com qualidade e segurança e fortalecem a reputação.

> [!question]- Quais tipos de teste a aula 1 cita para garantir o funcionamento em diferentes cenários?
> Unidade, integração, sistema e aceitação.

> [!question]- Mito 1: "testes são caros e demorados". Qual é a resposta da apostila?
> Testes adequados economizam tempo e dinheiro a longo prazo: corrigir defeitos cedo evita problemas maiores. A automação reduz o tempo e acelera o ciclo. → [[Mitos sobre Testes de Software]]

> [!question]- Por que o dev não deve ser o único a testar o próprio software?
> Porque tem uma visão enviesada. Testadores independentes trazem uma abordagem imparcial e exploram cenários que não foram considerados.

> [!question]- Testes garantem software 100% livre de erros?
> Não, é impossível. Eles mitigam riscos e dão alto grau de confiança, mas não garantem perfeição.

> [!question]- Testes devem ficar para o fim do ciclo?
> Não. Devem ser incorporados desde o início, porque testar continuamente evita retrabalho.

> [!question]- Caixa branca × caixa preta?
> Caixa branca: com conhecimento do código e da estrutura interna. Caixa preta: sem conhecimento detalhado do código ou da estrutura interna, com foco em entradas e saídas, a partir dos requisitos funcionais e das especificações. → [[Teste de Caixa Branca e Caixa Preta]]

> [!question]- Cite os tipos de teste de caixa branca da apostila.
> Cobertura de código, fluxo de controle, caminho básico e integração.

> [!question]- Cite os tipos de teste de caixa preta da apostila.
> Funcional, usabilidade, desempenho, segurança e estresse.

> [!question]- O que mede o teste de cobertura de código?
> Se todas as partes do código foram executadas e testadas: a cobertura de instruções, ramos (condicionais) e caminhos.

## Aula 2 - Testes de unidade
> [!question]- O que é um teste de unidade, e qual é o objetivo dele?
> Verificar o funcionamento de uma unidade do código (função, método, classe ou trecho). O objetivo é garantir que cada unidade funcione corretamente de forma isolada, antes da integração. → [[Teste de Unidade]]

> [!question]- Quais são os 4 benefícios dos testes de unidade?
> Detecção precoce de defeitos, facilitação da manutenção, documentação viva do código, e confiança e qualidade do software.

> [!question]- Cite as boas práticas de testes de unidade.
> Escrever os testes antes do código (TDD), manter os testes pequenos e rápidos, cobertura abrangente (incluindo casos de borda e de erro), automatizar, testar o comportamento esperado e o não esperado, e atualizar os testes conforme o código evolui.

> [!question]- Quais frameworks de teste .NET a aula apresenta?
> NUnit, xUnit e MSTest. → [[Frameworks de Teste .NET (NUnit, xUnit, MSTest)]]

> [!question]- Qual é o atributo do método de teste em cada framework?
> NUnit: `[Test]`. xUnit: `[Fact]`. MSTest: `[TestMethod]`.

> [!question]- Qual framework dispensa uma classe de teste especial?
> O xUnit, que tem uma descoberta de testes mais moderna. O NUnit usa `[TestFixture]` e o MSTest usa `[TestClass]`.

> [!question]- Quais frameworks são mais extensíveis?
> NUnit e xUnit. O MSTest tem menos opções de extensibilidade.

> [!question]- Quais são as três seções dos métodos de teste nos exemplos?
> Arrange, Act e Assert.

## Aula 3 - TDD
> [!question]- O que é TDD?
> Desenvolvimento Orientado a Testes: escrever testes automatizados antes da implementação do código, num ciclo de repetição. → [[TDD (Test-Driven Development)]]

> [!question]- Descreva as 3 etapas do ciclo do TDD.
> Red: escrever um teste para falhar, descrevendo o comportamento esperado. Green: implementar o código mínimo para o teste passar. Refactor: melhorar a qualidade e a legibilidade sem mudar o comportamento, e rodar o teste novamente.

> [!question]- No exemplo `IsAlphaString`, o que mudou na refatoração?
> O `foreach` foi substituído por LINQ (`input.All(c => char.IsLetter(c))`), mais conciso, com o mesmo comportamento.

> [!question]- O fluxo do TDD muda em cenários mais complexos?
> Não. É o mesmo Red → Green → Refactor.

> [!question]- Quais são os benefícios do TDD, segundo o resumo da aula?
> Maior confiabilidade do código, menor quantidade de defeitos e maior capacidade de refatoração.

## Aula 4 - Testes de integração
> [!question]- Por que os testes unitários não bastam?
> Porque testar cada parte isoladamente não garante que as partes funcionem integradas. O teste de integração verifica a comunicação e a troca de dados entre elas. → [[Teste de Integração]]

> [!question]- Que problemas o teste de integração encontra?
> Incompatibilidades entre componentes, erros de comunicação e falhas na passagem de dados.

> [!question]- Como deve ser o ambiente de teste de integração?
> Controlado e semelhante ao de produção, com bancos de dados, serviços externos e APIs. Virtualização ou containers (Docker) facilitam.

> [!question]- Top-Down × Bottom-Up: onde começa cada uma, e o que simula?
> Top-Down: começa pelos módulos mais externos e desce. Os módulos externos são simulados, ou se usam stubs para simular seu comportamento. Bottom-Up: começa pelos mais internos (baixo nível) e sobe. As dependências externas são simuladas, ou se usam mock objects.

> [!question]- O que é a estratégia Sandwich?
> A híbrida: combina top-down e bottom-up, testando os módulos superiores e inferiores ao mesmo tempo.

> [!question]- Quando o Big Bang é útil?
> Quando o sistema tem poucos módulos, ou quando os módulos são independentes entre si. Nele, tudo é integrado e testado de uma vez, sem abordagem incremental.

> [!question]- Quais são os 5 tipos de validação nos testes de integração?
> Interface, dados, fluxo de controle, comportamento e desempenho.

> [!question]- Quem realiza os testes de integração?
> Não há um responsável específico: a equipe de teste, os especialistas em desenvolvimento e a equipe de qualidade (QA). O importante é a colaboração.

## Aula 5 - BDD
> [!question]- O que é BDD, e qual a relação dele com o TDD?
> Desenvolvimento Guiado por Comportamento: foca na colaboração para construir o software a partir de comportamentos e requisitos de negócio claros. É uma evolução natural do TDD, ampliando o escopo para os testes de aceitação e integração. → [[BDD (Behavior-Driven Development)]]

> [!question]- Quais são os 4 princípios do BDD?
> Colaboração, linguagem ubíqua, testes como especificações e feedback rápido.

> [!question]- O que significa "testes como especificações"?
> Os cenários descrevem o comportamento esperado e viram especificações vivas: uma documentação executável e atualizada.

> [!question]- Cite as boas práticas do BDD.
> Identificar os cenários de uso, escrever os cenários de teste, automatizar, integrar à integração contínua e envolver as partes interessadas.

> [!question]- Quais palavras estruturam os cenários do exemplo do hotel?
> Dado, Quando, E, Então.

> [!question]- Quais ferramentas de BDD a aula cita?
> SpecFlow (para .NET), que permite escrever cenários de teste em linguagem natural, como o Gherkin, e executá-los de forma automatizada, e Cucumber (para várias linguagens).

## Aula 6 - Testes de carga
> [!question]- Teste de carga × teste de estresse?
> Carga: desempenho em condições normais, com o número esperado de usuários e transações, para achar gargalos e avaliar a estabilidade. Estresse: condições extremas, além dos limites, para achar os pontos de falha (recursos esgotados, tempo de resposta excessivo, comportamento inesperado). → [[Teste de Carga e Teste de Estresse]]

> [!question]- Quais são os benefícios do teste de carga?
> Melhora do desempenho, garantia da resiliência e prevenção de falhas.

> [!question]- JMeter: em que linguagem foi desenvolvido, e o que ele simula?
> Em Java (é de código aberto). Simula centenas ou milhares de usuários virtuais executando ações num período. → [[Ferramentas de Teste de Carga (JMeter e K6)]]

> [!question]- K6: qual é o destaque dele, e quais são os pré-requisitos?
> Consumo mínimo de recursos e alto desempenho, para testes de pico, estresse e absorção. Pré-requisitos: JavaScript básico e VS Code.

> [!question]- Como instalar o K6 no macOS, e como rodar um teste?
> `brew install k6`. Depois, `k6 run index.js`.

## Dúvidas em aberto
- [ ] O resumo da aula 2 diz que foram apresentadas "maneiras para criar mock", mas o texto do PDF não detalha. Vale conferir na videoaula.
- [ ] Os vídeos de Hands On não estão nos PDFs. Vale complementar com o que foi mostrado (projeto com baixa cobertura, TDD ao vivo, SpecFlow, JMeter e K6).

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
