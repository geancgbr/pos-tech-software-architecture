---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 5
fonte: "Aula 05 - Trabalhando com BDD.pdf"
---

# QS 05 - Trabalhando com BDD

← [[QS 04 - Testes de integração]] · [[Qualidade de Software]] · Próxima → [[QS 06 - Testes de carga]]

> [!summary] Em uma frase
> O [[BDD (Behavior-Driven Development)|BDD]] (Desenvolvimento Guiado por Comportamento) é uma **evolução natural do TDD**. Ele descreve o comportamento esperado do software em **cenários de uso**, numa linguagem que todos entendem, e amplia o escopo para testes de **aceitação e integração**.

## Hands On (vídeo)
BDD na plataforma .NET com o framework **SpecFlow**, que permite escrever cenários de teste em linguagem natural, como o **Gherkin**, e executá-los de forma automatizada.

## O que é
- Abordagem que integra as melhores práticas do desenvolvimento ágil, os testes automatizados e a comunicação eficiente entre desenvolvimento e negócio.
- Foca na **colaboração** entre devs, testadores e partes interessadas, para que o software seja construído a partir de **comportamentos e requisitos de negócio claros**.
- Em vez de olhar só para os testes de unidade, aborda o software **como um todo**. O fluxo está na Figura 1 do PDF (fonte: Rocha et al., 2019).

## Os 4 princípios
| Princípio | Ideia |
|---|---|
| **Colaboração** | Devs, testadores e partes interessadas com entendimento comum dos requisitos |
| **[[Linguagem Ubíqua]]** | Linguagem de domínio comum: cenários e testes compreensíveis por devs, usuários e partes interessadas |
| **Testes como especificações** | Os cenários descrevem o comportamento esperado e viram **especificações vivas**, uma documentação executável e atualizada |
| **Feedback rápido** | Pela automação e pela execução contínua dos cenários |

## Boas práticas
1. **Identificar os cenários de uso**: as necessidades dos usuários e as principais funcionalidades.
2. **Escrever os cenários de teste** na sintaxe do BDD, em termos de **entradas, ações e saídas**.
3. **Automatizar** com frameworks de BDD, para ter repetibilidade e consistência.
4. **Integração contínua**: executar os cenários regularmente, com feedback rápido.
5. **Envolver as partes interessadas** (usuários, analistas de negócio) na definição e na validação dos cenários.

## Exemplo da aula: reserva de quartos de hotel
> [!example] Cenário 1: Pesquisar quartos disponíveis
> - **Dado** que um usuário está na página inicial.
> - **Quando** o usuário preenche as datas de check-in e check-out.
> - **E** seleciona o número de hóspedes.
> - **Então** o sistema exibe uma lista de quartos disponíveis para as datas e o número de hóspedes informados.

> [!example] Cenário 2: Reservar um quarto
> - **Dado** que um usuário está visualizando os detalhes de um quarto disponível.
> - **Quando** o usuário clica no botão "Reservar".
> - **Então** o sistema solicita que faça login ou crie uma conta.
> - **E** o usuário realiza o login ou cria uma conta.
> - **Então** o sistema confirma a reserva e exibe uma mensagem de sucesso.

> [!example] Cenário 3: Cancelar uma reserva
> - **Dado** que um usuário está logado na sua conta.
> - **Quando** o usuário acessa a página de reservas.
> - **E** seleciona a reserva que deseja cancelar.
> - **Então** o sistema exibe uma confirmação de cancelamento.
> - **E** o usuário confirma o cancelamento.
> - **Então** o sistema cancela a reserva e exibe uma mensagem de confirmação.

Cada cenário descreve **um comportamento específico** a verificar.

**Ferramentas de automação**: **SpecFlow** (para .NET) e **Cucumber** (para várias linguagens). Com elas, o comportamento é validado continuamente, alinhado aos requisitos de negócio.

## Referências
Rocha et al., *Agile Teaching Practices: Using TDD and BDD in Software Development Teaching* (2019) · Smart e Molak, *BDD in Action*, 2ª ed. (2023)
