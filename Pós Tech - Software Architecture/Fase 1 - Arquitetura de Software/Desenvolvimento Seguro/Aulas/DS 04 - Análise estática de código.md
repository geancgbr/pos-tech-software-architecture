---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 4
fonte: "Aula 4.pdf"
---

# DS 04 - Análise estática de código

← [[DS 03 - Bibliotecas de software]] · [[Desenvolvimento Seguro]] · Próxima → [[DS 05 - OWASP e OWASP Top 10]]

> [!summary] Em uma frase
> A [[Análise Estática de Código|análise estática]] examina o código-fonte **sem executá-lo**, procurando problemas, vulnerabilidades, erros e oportunidades de otimização. Ela ajuda na [[Manutenibilidade|manutenibilidade]], e o [[SonarQube]] a integra ao pipeline de CI/CD.

## Hands On (vídeo)
O **SonarQube** na prática, integrado a uma **pipeline** de desenvolvimento como parte do ciclo de vida do software. Segundo o resumo da aula, o vídeo também mostra como avaliar **métricas de cobertura** e identificar vulnerabilidades.

## Manutenibilidade
- **Definição**: a capacidade de o código-fonte ser facilmente **compreendido, modificado, corrigido e estendido** ao longo do tempo. É crítica para o software continuar útil depois da implementação inicial.
- A manutenção é **inevitável**: os requisitos evoluem, entram recursos novos, aparecem bugs. O código deve permitir mudanças com o mínimo de esforço e risco.

| Prática | Ideia |
|---|---|
| **Clareza e legibilidade** | Nomes significativos, comentários explicativos, formatação consistente |
| **[[Modularização]]** | Módulos independentes, mais fáceis de entender, testar e modificar |
| **[[Teste de Unidade\|Testes unitários]]** | Problemas identificados cedo; alterações não introduzem bugs |
| **Gerenciamento de dependências** | Controle rigoroso de bibliotecas, para evitar conflitos e incompatibilidades |
| **Padrões de codificação** | Consistentes em toda a equipe |
| **Refatoração** | Eliminar código redundante ou complexo e melhorar a estrutura, de forma contínua |
| **Documentação adequada** | Além dos comentários, documentação externa da arquitetura, dos fluxos de dados e dos componentes |

Investir em manutenibilidade **desde o início** economiza tempo e recursos depois.

## Análise estática de código
- É um **processo automatizado** que examina o código **sem executá-lo**.
- Busca problemas potenciais, **vulnerabilidades de segurança**, erros de codificação e oportunidades de otimização.
- **Diferença para os testes dinâmicos**: nos testes dinâmicos, o código é executado e testado em tempo real. A análise estática avalia o código **em repouso**, antes de ele rodar.

**Abordagens das ferramentas**

| Abordagem | O que faz |
|---|---|
| **Léxica e sintática** | Primeira etapa: cria uma representação estruturada do programa e encontra erros de formatação e de sintaxe |
| **Fluxo de controle** | Examina como os dados fluem pelo código: caminhos de execução e problemas de lógica |
| **Dependências** | Rastreia as dependências entre partes do código: problemas de integração e de dependência de bibliotecas |
| **Segurança** | Encontra vulnerabilidades conhecidas, como **SQL Injection** e **XSS** |
| **Estilo de código** | Verifica as diretrizes: formatação, nomes de variáveis, boas práticas da linguagem |

## Ferramentas
| Ferramenta | Linguagem | O que verifica |
|---|---|---|
| **ESLint** | JavaScript | Estilo, erros de sintaxe e até vulnerabilidades. Muito usado na comunidade JS |
| **Pylint** | Python | Erros, problemas de estilo, diretrizes de codificação |
| **RuboCop** | Ruby | Problemas de estilo e erros comuns |
| **Checkstyle** | Java | Estilo, seguindo as convenções de codificação Java |
| **Cppcheck** | C/C++ | Erros de programação, **vazamentos de memória**, estilo |
| **SonarQube** | Várias (Java, C#, JavaScript, Python...) | Visão abrangente da qualidade: problemas, inconsistências, vulnerabilidades e otimizações. Altamente integrável a **CI/CD** |

Detalhes em [[SonarQube]].

## Referências
DevMedia, *Como adotar a análise estática de código* (2023) · Softplan, *Qualidade do código* (2022) · Tecnisys, *Benefícios do uso de ferramentas de análise de código estático* (2023)
