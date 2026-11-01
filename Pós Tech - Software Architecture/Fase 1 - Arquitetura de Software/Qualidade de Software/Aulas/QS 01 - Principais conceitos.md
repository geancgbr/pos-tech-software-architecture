---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 1
fonte: "Aula 01 - Principais Conceitos.pdf"
---

# QS 01 - Principais conceitos

[[Qualidade de Software]] · Próxima → [[QS 02 - Testes de unidade]]

> [!summary] Em uma frase
> Esta aula mostra por que testar ([[Testes de Software]]), derruba 5 [[Mitos sobre Testes de Software|mitos sobre testes]] e diferencia os [[Teste de Caixa Branca e Caixa Preta|testes de caixa branca e caixa preta]].

## Hands On (vídeo)
Pontos que mostram a necessidade de testar e as razões pelas quais os testes são essenciais para a qualidade e a confiabilidade dos sistemas.

## Por que testar
- A dependência crescente de software torna fundamentais a **qualidade** e a **confiabilidade**. Os testes permitem identificar e corrigir defeitos **antes** do lançamento.
- **Reflexão da aula**: confiamos em carros e há voluntários para viajar de foguete porque **confiamos nos testes** que as empresas fazem, como os testes de airbag e de cinto de segurança (Figura 1 do PDF).
- Empresas destroem carros, foguetes e equipamentos cirúrgicos para testar porque **a confiança é crucial**: o usuário precisa confiar que o software funciona como esperado e que suas informações estão seguras. Testes rigorosos mostram compromisso com qualidade e segurança e fortalecem a reputação da organização.
- **Finalidade dos testes**: descobrir erros de programação, falhas de lógica, comportamentos inesperados e vulnerabilidades de segurança.
- Com testes de **unidade, integração, sistema e aceitação**, garante-se que o software funcione em diferentes cenários e condições.
- **Resultado**: produto mais confiável e robusto, com menos bugs e menor probabilidade de falhas críticas. Os testes também avaliam o desempenho, para que o software seja rápido, eficiente e escalável.

## Os 5 mitos
| # | Mito | O que a apostila diz |
|---|---|---|
| 1 | "Testes são caros e consomem muito tempo" | Testes adequados **economizam** tempo e dinheiro a longo prazo: corrigir cedo evita problemas maiores e mais caros. A automação reduz o tempo de execução e acelera o ciclo |
| 2 | "O dev consegue testar o próprio software com eficácia" | O dev pode fazer testes iniciais, mas tem uma **visão enviesada**. Testadores independentes trazem uma abordagem imparcial e exploram cenários não considerados |
| 3 | "Testes garantem software 100% livre de erros" | **Impossível**. Os testes identificam a maioria dos defeitos, mitigam riscos e dão alto grau de confiança, mas não garantem perfeição |
| 4 | "Testes são só para empresas grandes ou projetos complexos" | São importantes para **todos os tamanhos** e complexidades. Até um app pequeno pode ter bugs que afetam o usuário |
| 5 | "Testes só podem ser feitos no fim do ciclo" | Devem ser incorporados **desde o início**. Testar continuamente evita retrabalho e mantém a qualidade |

## Caixa branca × caixa preta
As duas abordagens buscam qualidade, mas diferem na perspectiva e no **nível de conhecimento interno** do sistema.

| | Caixa branca (White Box) | Caixa preta (Black Box) |
|---|---|---|
| Base | Conhecimento da **estrutura interna e do código-fonte**. A pessoa testadora tem acesso ao código e à lógica | **Sem conhecimento detalhado** do código-fonte ou da estrutura interna. Foco exclusivo em **entradas e saídas**, avaliando o comportamento e a funcionalidade como um todo, com base nos requisitos funcionais e nas especificações |
| Tipos citados | Cobertura de código, fluxo de controle, caminho básico, integração | Funcional, usabilidade, desempenho, segurança, estresse |

A definição de cada tipo está em [[Teste de Caixa Branca e Caixa Preta]].

## Resumo da própria apostila
Detecção precoce de defeitos, garantia da qualidade, confiança do usuário e melhoria contínua da qualidade, além dos 5 mitos.

## Referências
Gabriela, L. *Por que e o que é possível testar?* (Alura, 2021) · Revista Carro, *Fiat Palio recebe só uma estrela em teste de segurança* (2016)
