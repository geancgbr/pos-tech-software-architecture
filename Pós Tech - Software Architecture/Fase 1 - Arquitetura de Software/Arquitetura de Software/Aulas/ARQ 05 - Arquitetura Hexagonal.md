---
tags: [pos-tech/fase-1, arquitetura, aula]
disciplina: Arquitetura de Software
aula: 5
fonte: "Aula 5 - Arquitetura de Software_revFinal.pdf"
---

# ARQ 05 - Arquitetura Hexagonal

← [[ARQ 04 - Escalabilidade, disponibilidade e desempenho]] · [[Arquitetura de Software]]

> [!summary] Em uma frase
> A [[Arquitetura Hexagonal]] (ou [[Portas e Adaptadores]]), proposta por Alistair Cockburn em meados dos anos 1990, aplica a [[Separação de Conceitos (SoC)]]. Ela isola a lógica de negócio no centro do hexágono, que se comunica com o mundo externo por portas (interfaces) e adaptadores (tecnologias), e usa [[Inversão de Controle (IoC)]] para que o centro não dependa da infraestrutura.

## Hands On (vídeos)
- O que é a arquitetura hexagonal e como ela ajuda no desenvolvimento e na manutenção.
- Portas, adaptadores e atores, com exemplos de código.
- Criação de **atores conduzidos** para cache e para persistência da entidade Usuários.
- O conceito de **Use Case** (muito conhecido em outras arquiteturas, como a Clean Architecture), com um exemplo de persistência de usuário.

## Separação de Conceitos (SoC)
- Princípio básico da engenharia de software: modularizar a solução para que cada módulo resolva **um único problema**.
- Normalmente aparece em softwares de grande porte ou em projetos com mais de uma linguagem.
- **Exemplo: MVC**. A **View** apresenta os dados, o **Model** trata o processamento (regras de negócio) e o **Controller** faz o intermédio entre os dois.

## A proposta de Cockburn
- Foi publicada na primeira wiki, a **WikiWikiWeb**, e modulariza a solução em **3 áreas isoladas**:
  - o **centro do hexágono**;
  - o **lado superior esquerdo**, fora do hexágono;
  - o **lado inferior direito**, fora do hexágono.
- **Objetivos** (parecidos com os da arquitetura limpa): reusabilidade de código, **alta coesão**, **baixo acoplamento**, **independência de tecnologia** e facilidade de teste.
- **Testes**: em algumas abordagens, o acoplamento entre camadas e frameworks impede fazer todos os testes básicos da pirâmide de testes (Figura 1 do PDF).
- **Foco**: isolar a lógica no centro, sem dependência de outras camadas ou tecnologias (qual banco, qual front-end). Assim, dá para trocar de tecnologia sem impactar as classes de domínio e os casos de uso. Exemplo: trocar a interface entre Web, mobile e API sem mexer no domínio.

## O centro: Application
- No desenho original (Figura 2 do PDF), o centro se chama **Application**. Ele **não tem relação** com a camada Application da arquitetura de camadas.
- É onde está o motivo principal de o software existir: o **core**, a camada de **domínio**, o coração do sistema.
- Contém modelos, domínios e regras de negócio, abstraindo as regras do mundo real em modelo de objetos.
- Deve ser **agnóstico** a tecnologia, framework e infraestrutura (interfaces gráficas, de comunicação, dispositivos externos). **Pode** depender de frameworks de serviços gerais, como log e IoC.

## Por que "hexagonal"
- O nome **não tem relação com o número 6**: a referência é ao polígono. Poderia ser um pentágono ou um heptágono.
- Os lados representam as diferentes implementações e tecnologias que a aplicação usa para expor seus resultados.
- Para Cockburn, cada face representa um motivo pelo qual o sistema precisa se comunicar com o mundo exterior. Por isso são hexágonos concêntricos, e não círculos concêntricos.
- Em **2005**, ele tentou renomear a arquitetura para **Portas e Adaptadores**: as faces do hexágono interno são portas, e os objetos entre os dois hexágonos são adaptadores. O nome "hexagonal" continuou mais conhecido.

## Portas, adaptadores e atores
| Elemento | O que é | Onde fica | Exemplos |
|---|---|---|---|
| **Porta** | Conceito lógico: ponto de entrada e saída. É uma **interface de programação** usada para falar com os casos de uso | **Centro** (portas são independentes de tecnologia) | `public interface ICadastroPessoa{}` (C#) |
| **Porta de entrada** | Comunicação **de fora para dentro**: declara os serviços **providos** pelo sistema | Centro | Uma classe externa chamando um caso de uso |
| **Porta de saída** | Comunicação **de dentro para fora**: declara os serviços **requeridos** pelo sistema | Centro | Interação com banco de dados |
| **Adaptador** | Tecnologia externa que implementa a conexão entre a porta e o serviço externo. São os "plugues" (como um adaptador de tomada "Benjamin" ou "T") | Fora do hexágono | HTTP/REST, gRPC, GraphQL, SQL, NoSQL, web, mobile |
| **Ator condutor** | Recebe chamadas de fora e as encaminha às **portas de entrada** | Lado **esquerdo** | Requisição HTTP, suíte de testes, API, app mobile, terminal/CMD, páginas web |
| **Ator conduzido** | Recebe chamadas **de dentro** (dos casos de uso) e as direciona a um sistema externo. É acionado pelo centro por **portas secundárias** | Lado **inferior direito** | Banco de dados, SMTP, sistema de arquivos, HTTP, serviços de terceiros |

- Classificação das portas: Marco Tulio Valente, *Engenharia de Software Moderna*.
- **Pelo menos dois adaptadores por porta**: um para teste e um para a implementação real. Exemplo: uma porta de cache com um adaptador **Redis** e outro de **cache em memória**, para os testes unitários.
- **Tipos de ator conduzido**:
  - **Repositório** (*Repository*): **envia e recebe** informações. Exemplo: banco de dados.
  - **Destinatário** (*Recipient*): **envia e esquece**. Exemplo: e-mail SMTP.

Detalhes em [[Portas e Adaptadores]] e [[Atores Condutores e Conduzidos]].

## Fluxo de execução
1. Um **adaptador externo** recebe a solicitação e adapta os dados para a estrutura esperada pela camada de negócios.
2. O adaptador envia a solicitação para uma **porta** na camada de negócios.
3. A porta executa a lógica de negócio, interagindo com entidades e serviços.
4. A porta envia a resposta para **outro adaptador externo**, que a adapta para a interface que originou a solicitação.
5. O adaptador devolve a resposta à interface externa, que a apresenta ao usuário.

> [!warning] O problema do fluxo e a solução
> Nesse fluxo, o **centro passa a depender do lado direito** (dos atores conduzidos), enquanto os conduzidos não dependem de ninguém. Cockburn resolveu isso aplicando a **[[Inversão de Controle (IoC)]]**.

## Inversão de Controle (IoC)
- Princípio de design em que a sequência (o controle) das chamadas de métodos é **invertida** em relação à programação tradicional: não é determinada diretamente pelo programador.
- O controle é **delegado a uma infraestrutura**, muitas vezes chamada de **contêiner**, ou a outro componente que assume a execução. É comum em frameworks.
- É um padrão utilizado em projetos orientados a objetos, que utilizam conceitos como interface, herança e polimorfismo.

## Resumo da própria apostila
- 3 áreas: centro do hexágono, lado esquerdo e lado direito.
- A separação em camadas ajuda nos testes.
- Na camada de aplicação ficam as regras de negócio, que podem ser definidas por **casos de uso**.
- Fora do hexágono, os adaptadores se comunicam com o centro por portas, que são interfaces de linguagem de programação.
- Tipos de portas e adaptadores; atores condutores e conduzidos; fluxo de execução; introdução ao IoC.

## Referências
Branas, *Hexagonal Architecture (Ports and Adapters) with Alistair Cockburn*, Live #98 (YouTube, 2022) · Valente, *Engenharia de Software Moderna* (2020) · Shrivastava e Srivastav, *Solutions Architect's Handbook*, 2ª ed. (2022)
