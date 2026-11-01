---
tags: [pos-tech/fase-1, arquitetura, aula]
disciplina: Arquitetura de Software
aula: 3
fonte: "Aula 3 - Arquitetura de Software_revFinal.pdf"
---

# ARQ 03 - Documentação, testabilidade e modificabilidade

← [[ARQ 02 - Processo e modularização]] · [[Arquitetura de Software]] · Próxima → [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]]

> [!summary] Em uma frase
> [[Documentação de Software|Documentação]], [[Testabilidade]] e [[Modificabilidade]] são pilares de uma boa arquitetura que influenciam a qualidade do software. São passos simples que, adotados desde o início, são fáceis de manter ao longo do desenvolvimento.

## Hands On (vídeos)
- Tipos de documentação e como eles ajudam do levantamento de requisitos à manutenção e ao desenvolvimento de novas funcionalidades.
- **Swagger** e **Redoc**: ferramentas para criar documentação.
- Testes: o teste do "caminho feliz" num sistema legado e o teste correto usando **[[BDD (Behavior-Driven Development)|BDD]]**.
- Modificabilidade: exemplos práticos de como é difícil atualizar um legado construído sem muitos requisitos, e como fica simples quando o desenvolvimento começa pelos pontos vistos nos vídeos anteriores.

## Documentação: 4 tipos
| Tipo | Para quem e para quê | Exemplos |
|---|---|---|
| **Utilização do projeto** | Usuários finais (e membros do time que precisam conhecer o software): como usar | Manual do usuário com instruções passo a passo, imagens, vídeos, fluxogramas |
| **Desenvolvimento do projeto** | Time de desenvolvimento: registra o processo, da concepção à entrega (tecnologias, decisões de arquitetura e design, testes, bugs, soluções) | Documento da arquitetura com camadas, componentes e comunicação; relatório de testes (unitários, integração, funcionais, desempenho) |
| **Infraestrutura** | Manutenção e gerenciamento da infraestrutura de TI (hardware, software, rede); garante que a configuração dos ambientes de desenvolvimento e produção seja consistente e adequada | Inventário de hardware, inventário de software, diagramas de rede, políticas e procedimentos, documentação de configuração, relatórios de monitoramento |
| **Arquitetura do projeto** | Estrutura e design do software, para facilitar desenvolvimento, manutenção e evolução; garante que o software seja escalável | Visão geral, diagramas de arquitetura, padrões de design, descrição dos componentes, interfaces do sistema, decisões de design |

Detalhes de cada item em [[Documentação de Software]].

## Testabilidade
- **Definição**: capacidade de o software ser **testado de maneira eficaz**, ou seja, avaliado com facilidade quanto a qualidade, funcionalidade e desempenho. Inclui a facilidade de criar, executar e manter testes.
- **Importância**: sem testes adequados, é difícil garantir que o sistema atende aos requisitos. Quanto mais testável, menos tempo e recursos para testar, o que reduz custo e prazo.
- **Fatores**: design de software, arquitetura de software, instrumentação de código, dados de teste, ferramentas de teste e acessibilidade de interfaces.
- Deve ser tratada como **requisito importante**, não como processo secundário ou opcional.

## Modificabilidade
- **Definição**: capacidade de o software ser **modificado facilmente**: alterado, mantido e evoluído para novos requisitos e necessidades.
- **Importância**: o software precisa mudar com frequência (corrigir defeitos, melhorar funcionalidades, novos requisitos, novos ambientes). Modificar de forma eficiente reduz tempo e custo, melhora a qualidade e mantém o sistema atendendo o usuário.
- **Fatores**: design de software, arquitetura de software, qualidade do código, documentação e testabilidade.
- Também deve ser considerada um **requisito importante** do software.

Detalhes dos fatores em [[Testabilidade]] e [[Modificabilidade]].

## Referências
Aniche, *Test-driven Development* (2013) e *Testes Automatizados de Software* (2015) · Vazquez e Simões, *Engenharia de requisitos* (2016)
