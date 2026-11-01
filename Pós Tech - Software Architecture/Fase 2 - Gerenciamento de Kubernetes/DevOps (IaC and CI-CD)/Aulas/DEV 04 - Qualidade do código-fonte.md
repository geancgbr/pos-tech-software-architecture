---
tags: [pos-tech/fase-2, devops, aula]
disciplina: DevOps (IaC and CI/CD)
aula: 4
fonte: "Aula 4 - DevOps - Qualidade do código-fonte_revFinal.pdf (Fabiano da Silva Carneiro)"
---

# DEV 04 - Qualidade do código-fonte

← [[DEV 03 - Testes automatizados com CI]] · [[DevOps (IaC and CI-CD)]]

> [!summary] Em uma frase
> A [[Qualidade do Código-Fonte|qualidade do código-fonte]] mede quão bem escrito, organizado, eficiente e confiável é o código. Ela é garantida no DevOps com TDD, CI, code review e **ferramentas de análise estática** (como o **SonarQube**) integradas ao pipeline, que têm limitações e desafios extras em código legado.

## Hands On (vídeo)
Integrar o **SonarQube** ao pipeline DevOps: criar **Quality Profiles** e **Quality Gates**, sincronizar com a esteira do GitHub e ver os resultados. O PDF traz o link "Códigos da aula 4".

## Por que importa
- O código-fonte é a base de qualquer programa. **Código de baixa qualidade** leva a erros, bugs, vulnerabilidades de segurança, dificuldade de manutenção, atrasos e baixa escalabilidade.
- A qualidade deve ser considerada **em todo o processo**, do planejamento aos testes e à implantação.

## O que é qualidade do código-fonte
Uma medida de **quão bem escrito, organizado, eficiente e confiável** é o código, e da sua capacidade de atender aos requisitos **funcionais e não funcionais** de forma eficaz e sustentável. Afeta a manutenção, a escalabilidade, a confiabilidade e o desempenho.

| Característica | O que significa |
|---|---|
| **Legibilidade** | Nomes significativos, comentários adequados, estrutura clara |
| **Eficiência** | Bom uso de memória e processamento; sem redundância; loops e algoritmos otimizados |
| **Confiabilidade** | Tratamento de erros, validação de entradas e saídas, testes adequados |
| **Escalabilidade** | Lidar com mais carga e mais dados sem degradar desempenho ou confiabilidade |
| **Manutenibilidade** | Estrutura modular e organizada; adicionar, corrigir e atualizar sem impacto indesejado |
| **Segurança** | Prevenir vulnerabilidades conhecidas, proteger dados sensíveis, autenticar adequadamente |

## Como garantir no DevOps
- **Práticas ágeis**: **TDD** e **integração contínua**, com o código testado e validado continuamente.
- **Ferramentas** de automação de testes e de **análise estática** (segurança, performance, legibilidade).
- **Colaboração**: **code reviews**, **pair programming** e **sessões de depuração conjunta**.
- **Ferramentas de revisão de código** incorporadas à CI, com **feedback rápido**.

## Exemplos de baixa qualidade
Duplicação de código · falta de coesão · complexidade excessiva · falta de documentação · falta de validação de entrada (vulnerabilidades) · ausência de testes automatizados · falta de otimização · uso inadequado de variáveis (nomes confusos) · falta de modularização (um grande bloco monolítico) · uso excessivo de condicionais aninhados · falta de tratamento de exceções.

## Desafios da validação automática
| Desafio | O que acontece |
|---|---|
| **Configuração incorreta** | Resultados imprecisos ou problemas não detectados |
| **Falso positivo** | Aponta um problema que não existe e faz perder tempo |
| **Falso negativo** | Deixa passar um problema real |
| **Personalização limitada** | Poucas regras ou pouca adaptação ao ambiente |
| **Demora na execução** | Em projetos grandes, afeta a produtividade |
| **Dependência de versão** | As regras mudam entre versões, o que dificulta migrar |
| **Uso incorreto dos dados** | Interpretar mal os resultados leva a ações erradas |

## Código legado
**Código legado**: antigo, muitas vezes desatualizado, mas ainda em produção. Os desafios extras:
- **difícil integrar** as ferramentas (linguagem antiga ou versão obsoleta);
- **limitações na detecção** de problemas;
- **mais problemas** encontrados, o que gera sobrecarga;
- **restrições de tempo e orçamento** para corrigir tudo.

A abordagem deve ser **estratégica**: priorizar os problemas, alocar recursos e mirar a modernização, que é um **processo gradual**.

## Ferramentas de mercado
A escolha depende das necessidades do projeto, da linguagem e das preferências da equipe.

| Ferramenta | Para quê |
|---|---|
| **SonarQube e SonarCloud** | Análise estática: qualidade, vulnerabilidades, conformidade |
| **ESLint** | JavaScript: qualidade, erros de sintaxe e estilo |
| **PMD** | Várias linguagens (Java, JavaScript, Ruby, Apex): código duplicado, vulnerabilidades |
| **Checkstyle** | Java: estilo, convenções, vulnerabilidades |
| **CodeSonar** | Análise estática em C/C++, Java, JavaScript e Python: qualidade, vulnerabilidades, conformidade |
| **ReSharper** | Extensão do Visual Studio para C# e .NET: sintaxe, estilo, duplicação, vulnerabilidades |
| **FindBugs** | Java: bugs e vulnerabilidades |
| **PyLint** | Python: sintaxe, estilo e segurança |

A validação deve ser **regular ao longo de todo o ciclo de vida**. Investir em qualidade economiza tempo e recursos no futuro.

## Referência
Duvall, Matyas e Glover, *Continuous Integration* (2007)
