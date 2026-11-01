---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 3
fonte: "Aula 3.pdf"
---

# DS 03 - Bibliotecas de software

← [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]] · [[Desenvolvimento Seguro]] · Próxima → [[DS 04 - Análise estática de código]]

> [!summary] Em uma frase
> Ao importar uma biblioteca, você adiciona um componente crítico ao projeto. É preciso checar a [[Licenças de Software|licença]] (o que se pode usar, modificar e distribuir) e a [[Segurança de Bibliotecas de Terceiros|segurança]] (código malicioso, vulnerabilidades).

## Hands On (vídeo)
Num cenário real, como **importar uma biblioteca com segurança** e como **analisar a licença** antes de importá-la. O professor usa um projeto compartilhado com a turma.

## Por que a licença importa
Licenças de software são **acordos legais** que definem os direitos e as restrições de uso. A licença da biblioteca afeta sua capacidade de distribuir, comercializar e manter o software.

- **Compatibilidade de licenças**: as licenças das bibliotecas devem ser compatíveis com a do seu projeto, para evitar conflitos e problemas legais.
- **Responsabilidade legal**: bibliotecas com licenças inadequadas podem violar direitos de terceiros e levar a ações legais.
- **Liberdade de uso**: para promover uso e modificação livres, escolha licenças de código aberto que permitam isso. Para proteger propriedade intelectual, licenças mais restritivas.

## Licenças mais populares
| Licença | Característica |
|---|---|
| **MIT** | Muito usada em código aberto, conhecida pela **permissividade**: permite usar, modificar e distribuir, desde que o **aviso de direitos autorais e a licença original sejam mantidos** |
| **Apache** | Semelhante à MIT, mas com disposições para **proteger os contribuintes de responsabilidade legal** |
| **BSD** | Semelhante à MIT, com algumas variações nos detalhes |
| **GPL** (GNU) | Exige que o **software derivado também seja distribuído sob a GPL**. Por isso pode afetar a licença do seu próprio projeto |

## Riscos ao importar bibliotecas
O problema aqui não é a licença, e sim **importar sem analisar**: há riscos de segurança e confiabilidade.

> [!example] Caso UA-Parser-JS (CISOAdvisor, 2021)
> Pacote NPM usado para detectar dispositivo, navegador e SO a partir do *user agent*, com cerca de **24 milhões de downloads** no mês e **8 milhões por semana**. Três versões foram contaminadas com código para **minerar a criptomoeda Monero**, segundo o mantenedor no GitHub e um alerta da CISA (agência de segurança cibernética dos EUA).

**Cryptominer e cryptojacking**
- **Cryptominer**: programa ou script malicioso que usa a CPU ou a GPU do computador para **minerar criptomoedas sem o consentimento do dono**.
- **Mineração**: resolver cálculos complexos para validar transações numa blockchain, em troca de criptomoeda.
- **Cryptojacking**: a prática maliciosa de explorar o processamento de máquinas alheias, **sem consentimento ou conhecimento**, o que costuma causar lentidão e sobrecarga.
- Entram por malwares, scripts web maliciosos ou apps infectados, e podem minerar Bitcoin, Monero, Ethereum etc.

## Como garantir que a biblioteca é segura
**Dicas**
- Use **fontes confiáveis**: repositórios oficiais e desenvolvedores renomados.
- Bibliotecas **populares** costumam ter mais revisões e auditorias. Veja o número de downloads e a comunidade.
- Faça **auditorias de código**, internas ou com especialistas.

**Estratégias de validação**
- **Testes de segurança regulares** no projeto, incluindo as bibliotecas.
- Acompanhe as **vulnerabilidades conhecidas**. Serviços como o **`npm audit`** (Node.js) ajudam.
- Mantenha bibliotecas e pacotes **atualizados**, para ter as correções de segurança.
- Use ferramentas de **[[Análise Estática de Código|análise estática de código]]**.

## Referências
EVEO, *Licença de software* (2022) · UFPR, *Tipos de licenças de software* (2020) · VCX Solutions, *Licenciamento de software* (2022)
