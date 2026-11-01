---
tags: [pos-tech/fase-2, devops, aula]
disciplina: DevOps (IaC and CI/CD)
aula: 1
fonte: "Aula 1 - DevOps - CI-CD - Principais Conceitos_revFinal.pdf (Fabiano da Silva Carneiro)"
---

# DEV 01 - CI/CD: principais conceitos

[[DevOps (IaC and CI-CD)]] · Próxima → [[DEV 02 - Melhores práticas com o GitHub]]

> [!summary] Em uma frase
> O [[DevOps]] promove, por uma cultura de colaboração, desenvolvimento e manutenção com foco em qualidade, e a **[[Integração Contínua (CI)|integração contínua]]** é a base de toda a automação. **CD** junta dois processos: **[[Entrega Contínua e Deploy Contínuo|entrega contínua e deploy contínuo]]**.

## Hands On (vídeo)
Da origem do desenvolvimento de software à cultura DevOps; como as ferramentas funcionam juntas, de forma automatizada, na integração, entrega e implantação contínuas; e como criar um processo de integração contínua no **GitHub**. O PDF traz o link "Códigos da aula 1".

## Contexto
- Grandes empresas buscam **maximizar a eficiência das equipes, eliminando processos manuais e repetitivos**.
- **A base do sucesso de um projeto é a qualidade** com que ele foi desenvolvido. Boa parte do tempo vai para testes, com equipes cada vez maiores, o que é custoso em tempo e dinheiro. Por isso a aula traz conceitos avançados de testes na integração contínua, como o **TDD**, que aplica os testes desde o início da construção (Humble, 2014).
- **Métodos ágeis**: metodologias para que o desenvolvimento de sistemas se mantenha produtivo e evolucional.
- Como evitar que os devs sejam o **gargalo** da entrega, com até dezenas deles no mesmo projeto?

## Integração contínua
- Técnica que otimiza o desenvolvimento: os devs colocam o código num **único repositório**, para eliminar problemas e retrabalho e facilitar a localização de erros (Pires, 2019).
- Está contida no **Extreme Programming (XP)**, metodologia ágil criada em **1996** por **Kent Beck**. O XP usa a CI para unificar o trabalho dos devs e entrou no mercado como resposta ao desenvolvimento de sistemas, que exigia entregas mais rápidas (Kim et al., 2018).

**As "Boas Práticas de XP"** (Beck, 2004). Detalhes em [[Extreme Programming (XP)]].
| Prática | Ideia |
|---|---|
| Cliente sempre disponível | Participação constante: requisitos, dúvidas, ideias, prioridades |
| Uso de metáforas | "Apelidos" comuns à equipe, para fluir a comunicação |
| Planejamento do jogo | Reuniões com todos, inclusive o cliente, que organizam os requisitos em "histórias de clientes" e montam o cronograma para entregar rápido |
| Pequenas versões | Entregas pequenas, para o cliente validar e pedir alterações |
| Simplicidade de projeto | Código o mais simples possível, fácil de manter por qualquer membro |
| Melhoria constante | A cada versão, partes do código são melhoradas |
| Testes de aceitação | Regras definidas pelo cliente; sem elas funcionando, o projeto não é aceito |
| Testes em primeiro lugar | Pensar primeiro nos testes ("testes unitários de código"), que validam os critérios do cliente e os erros de programação |
| **Integração contínua** | "Juntar" as partes de todos num único local para testar o software completo. **Cada dev integra seu código ao menos uma vez por dia**, o que torna os defeitos fáceis de identificar enquanto o software ainda está em construção |

## Fluxo manual × automatizado
O fluxo manual (Quadro 1) é suscetível a erros:

| Etapa | O que é |
|---|---|
| Integração do código-fonte | "Juntar" o código de todos no mesmo repositório |
| Compilação ou build | Transformar o código-fonte em software "executável" |
| Verificação ou testes | Testar se o código está sem erros e integrado às partes dos outros |
| Implantação ou deploy | Instalar o software num servidor para os usuários acessarem |

- A CI propõe **automatizar** parte do desenvolvimento, para que os processos rodem **independentemente da vontade do desenvolvedor** e do modelo de desenvolvimento (Kim et al., 2018).
- Empresas ainda usam o modelo manual por **não estarem amadurecidas** para implantar testes efetivos e automatizados.
- **Paul Duvall** (*Continuous Integration*, 2007): a CI não é só juntar componentes. É **a peça central do desenvolvimento**, porque garante a integridade do software executando **um build a cada mudança**.

**Valores da CI** (Quadro 2, adaptado de Duvall, Matyas e Glover)
| Valor | Por quê |
|---|---|
| Redução de riscos | Integrar muitas vezes ao dia facilita detectar defeitos |
| Redução dos processos manuais repetitivos | Economiza tempo, custo e esforço, e minimiza erros |
| Gerar software implantável a qualquer momento | Os erros são comunicados na hora, não numa fase posterior |
| Maior visibilidade do projeto | Com tudo automatizado, há métricas de qualidade e do que falta entregar |
| Maior confiança no software produzido | Os devs são avisados de imediato se algo der errado |

## Entrega contínua × deploy contínuo
- **Entrega contínua**: cada mudança **pode** ser implantada em produção, mas a equipe pode optar por não fazer (geralmente por **motivos comerciais**). O pacote fica **pronto, testado e armazenado num repositório de artefatos**.
- **Deploy contínuo**: cada pacote é implantado **automaticamente em produção, sem intervenção humana**, assim que cumpre todos os requisitos da esteira (qualidade, segurança etc.).
- **Para haver deploy contínuo, é preciso ter entrega contínua.**

## Trabalhar em pequenos lotes
- Trabalha-se em grandes lotes por causa do **grande custo fixo** de entregar as alterações.
- Um objetivo chave da entrega contínua é **tornar viável economicamente trabalhar em pequenos lotes**. Isso reduz o tempo de feedback, facilita a triagem e a correção, aumenta a eficiência e a motivação e evita a **falácia do custo irrecuperável**.
- Pequenos lotes também **reduzem o risco da mudança** (Figura 2 do PDF).

## Referências
Beck, *Extreme Programming Explained* (2004) · Duvall, Matyas e Glover, *Continuous Integration* (2007) · Humble e Farley, *Entrega Contínua* (2014) · Kim et al., *Manual de DevOps* (2018) · Pires e Militão, *Integração contínua com Jenkins* (2019)
