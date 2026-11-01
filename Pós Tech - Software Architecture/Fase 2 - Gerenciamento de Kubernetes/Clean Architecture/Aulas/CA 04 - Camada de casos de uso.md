---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 4
fonte: "Aula 4.pdf (Erick Muller)"
---

# CA 04 - Camada de casos de uso

← [[CA 03 - Camada de entidades]] · [[Clean Architecture]] · Próxima → [[CA 05 - Adaptadores de interface e frameworks e drivers]]

> [!summary] Em uma frase
> Os [[Casos de Uso|casos de uso]] são o **"cérebro"** do software: cada um implementa **uma única regra de negócio**, isolada e testável. Recebem os dados e as dependências por **injeção de dependência e interfaces**, usam as **entidades** como abstração dos atores e podem ser testados com **[[Mock|mocks]]**, antes de qualquer interface externa.

## Hands On (vídeos)
Um papo com vários exemplos sobre a centralidade dos casos de uso como **orquestradores da regra de negócio** e como eles se relacionam com o resto da arquitetura. O PDF traz um link para uma base de dados da aula, para treinar.

## Casos de uso como ferramenta
- Documentar as necessidades do software como "casos de uso" é uma ideia antiga, presente em metodologias de construção e de gestão de processos de software, com modelos e livros dedicados.
- **Um caso de uso documenta um processo de negócio**: os dados necessários, os passos, as **exceções** e como tratá-las, e o **resultado**.
- **Em metodologias ágeis**: com casos de uso, implementa-se **só o necessário, não o desejado**. Por isso os cards de implementação costumam ser baseados neles.

## Casos de uso como camada
- No diagrama (Figura 1 do PDF), a camada de casos de uso fica **entre a de entidades e a de controllers**.
- Entrega as funcionalidades aos elementos externos e **centraliza a implementação das regras de negócio**.
- **O isolamento permite**:
  - cada regra num código **único, testável e utilizável** por outros casos de uso ou pelas camadas externas;
  - novas regras **sem risco** para as que já existem;
  - separar o **núcleo** (o que o software faz) das camadas **técnicas** (comunicação com o mundo exterior).

> [!warning] "O que" × "como": a apostila não é consistente
> Nesta aula, o texto diz que as duas camadas internas definem "o que" o software faz, **enquanto a camada de casos de uso define "como"**. Mas o resumo da mesma aula diz que, **com os casos de uso e as entidades, isolamos "o que" o software faz**. A aula 3 trata as camadas internas (Casos de Uso e Entidades) como o "o que", e a aula 7 chama de "quê" os componentes das regras de negócio que entregam as funcionalidades.

## Regras da camada (seguindo o SOLID)
1. **Cada implementação resolve um único caso de uso.** Um caso de uso **não pode**, por exemplo, criar um Estudante a partir de uma Pessoa **e** matricular esse Estudante: nesse caso, deve emitir um erro dizendo que o dado (Pessoa) recebido é inválido. Casos complexos se dividem em casos menores, e as chamadas entre eles são **explícitas**.
2. **Agrupamento** em classes, módulos, bibliotecas ou pacotes, por uma regra **coerente** (ex.: todos os casos de uso de matrícula num pacote). Numa classe, como **métodos estáticos**, porque os casos de uso funcionam de forma independente, **sem dividir estado**.
3. **Usar as entidades** como abstração dos atores, **nunca os dados crus** recebidos de quem instanciou. Criar as entidades já valida os dados.

## As três partes de um caso de uso
1. **Dados recebidos**: um tipo de dados próprio (que pode ser uma interface, para padronizar o acesso) ou uma instância de entidade.
2. **Algoritmo interno**: a funcionalidade.
3. **Retorno**: no exemplo, um objeto Estudante, definido na camada de entidade. Isso não viola a regra das camadas, porque quem usa é "externo" à camada de entidades. Algumas implementações retornam um **objeto de dados (DAO)**, mais como interface de comunicação (como uma porta) do que como imposição da Arquitetura Limpa.

**Exemplo da aula: registrar um Estudante** (o código está nas Figuras 2 e 3 do PDF)
- Registrar um estudante é criar um Estudante a partir de uma Pessoa existente.
- Na segunda versão, o caso de uso **recebe uma instância do repositório** para verificar se a Pessoa já é Estudante. É a **Inversão de Dependência** aplicada: dá para passar um **repositório "falso"** e testar a regra. Se funcionar, qualquer erro está no repositório, não no código.
- Ele usa **outro caso de uso** para verificar se a Pessoa já é Estudante.
- O objetivo é só **criar e validar o objeto**, não gravar no repositório. Provavelmente, quem chamou é que grava, usando o Repositório por meio de um Adapter.

## Casos de uso para teste
- Com um caso de uso pronto, já dá para testá-lo: inicializar uma entidade manualmente, criar um **"mock"** do repositório e validar.
- **Mock**: um objeto que se comporta exatamente como a interface pede e retorna os dados necessários para o teste. Não tem correspondente em português; já se usou **"fantoche"**, um objeto que "se comporta como" um real, mas manipulado para um propósito específico. Veja [[Mock]].
- **Vantagem**: testar as regras de negócio **antes de conectar** as interfaces externas. O software faz o que precisa, independentemente de vir de uma API, de uma GUI ou de outra interface ainda desconhecida.

## Resumo da própria apostila
A camada de casos de uso centraliza as regras de forma independente do uso. É um conceito **radical**: cada caso de uso, implementado como uma unidade, responde só pela funcionalidade esperada e **não depende de nenhum mecanismo externo**.

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008) · Fowler, *UseCase* (martinfowler.com)
