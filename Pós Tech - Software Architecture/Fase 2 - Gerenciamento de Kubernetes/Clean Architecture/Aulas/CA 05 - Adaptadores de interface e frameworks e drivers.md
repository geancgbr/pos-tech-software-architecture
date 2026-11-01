---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 5
fonte: "Aula 5.pdf (Erick Muller)"
---

# CA 05 - Adaptadores de interface e frameworks e drivers

← [[CA 04 - Camada de casos de uso]] · [[Clean Architecture]] · Próxima → [[CA 06 - Componentes]]

> [!summary] Em uma frase
> As duas camadas externas fazem o software se comunicar com o mundo real. Os **Adaptadores de Interface** ([[Controllers, Presenters e Gateways]]) intermediam e adaptam os dados nos dois sentidos. **Frameworks e Drivers** é a camada mais externa, com APIs, servidor, telas e acesso a dados.

## Hands On (vídeos)
O papel das duas camadas que fazem a interface com o "mundo real", e por que separá-las é vital: a regra de negócio não pode se misturar com os controles de operação nem com os serviços externos. O PDF traz um link para uma base de dados da aula.

## Por que essas camadas existem
Até aqui, o foco era o **domínio**. Mas o software precisa falar com o mundo exterior para ser usado. Quanto mais **externa** a camada, mais **perto do usuário** e do mundo exterior.

## Adaptadores de Interface (Interface Adapters)
- Fazem a **intermediação** entre os elementos externos e os internos: recebem a chamada de uma API e chamam o caso de uso.
- **Adaptam** os dados das camadas externas e **devolvem** corretamente a resposta.
- Os clientes externos **não acessam os casos de uso diretamente**: toda requisição é adaptada **na recepção e na entrega**. As camadas externas não preparam os dados, e os casos de uso não adaptam dados.
- **Padronizam o acesso** aos casos de uso: o cliente acessa um componente dessa camada, que se coordena com outros para adaptar a entrada, chamar o caso de uso e adaptar a saída.

> [!example] Duas analogias
> **Balconista de lanchonete**: o cardápio já existe, você escolhe e no máximo pede pequenas alterações. O pedido é adaptado para a cozinha e volta num formato padrão. O balcão é só um ponto de processamento entre duas camadas.
> **Vendedor de loja de roupas**: precisa entender o que você quer e escolher, entre as opções, o que atende. Do mesmo jeito, o cliente pode mandar os dados num formato diferente do que o caso de uso espera, ou esperar outro formato de retorno. Por isso a camada precisa saber **ajustar os dados e adaptar a resposta a cada cliente**.

### Os três tipos de componente
| Componente | Papel | Exemplo da aula |
|---|---|---|
| **Controller** | **Conector** entre as camadas de cima e de baixo; organiza os passos da requisição, instanciando e executando o necessário. Não precisa saber **como** o caso de uso funciona, só como ele recebe e devolve os dados. Para ele, não existe "sucesso" ou "erro": é um **"mensageiro"** | Na universidade: recebe os dados da pessoa e da disciplina, transforma em entidades, chama **MatricularAluno**, recebe o retorno e prepara a resposta |
| **Presenter** | Uma única finalidade: **preparar os dados de retorno** ao cliente que acessou o Controller, no modelo que ele entende. Normalmente é **instanciado pelo Controller** e usado só dentro da camada de Adapters | Numa API HTTP RESTful: os padrões HTTP, os cabeçalhos corretos, o conteúdo formatado conforme o cabeçalho Content |
| **Gateway** | Implementa a comunicação com **componentes externos** que fornecem ou armazenam dados ou executam atividades (ex.: permite aos casos de uso acessar repositórios). Cria uma forma intermediária e expõe **ações como atividades**, não como funções de baixo nível do serviço externo. É recebido pelo caso de uso **via injeção de dependência** | O `EstudanteGateway`, abaixo |

```typescript
class EstudanteGateway {
  obterEstudatePorPessoa(PessoaEntity): EstudanteEntity {
    // ...
  }
}
```

## Frameworks e Drivers
- É a camada **mais externa**: representa o mundo exterior. Usa as tecnologias, bibliotecas e funções que falam com o mundo real.
- Aqui ficam:
  - as **rotas da API** e o **servidor**, além do tratamento dos dados de cada cliente;
  - as regras de implementação, não de negócio: como a API funciona, segurança, **autenticação e autorização**;
  - as **interfaces com as origens de dados**: repositórios, APIs externas, ferramentas;
  - numa aplicação desktop, as **telas e os botões**, que chamam os Controllers;
  - as conexões com repositórios, **injetadas ao chamar um Controller**, e os controles de erro dos serviços externos.
- **Analogia**: se o software fosse um computador, essa camada seria a **tela, o teclado e as portas**. São essenciais para usá-lo, mas não fazem parte do funcionamento interno. Não é o teclado que executa o trabalho, mas sem ele não dá para dizer ao computador o que fazer.
- **Isolamento de erros**: se um serviço de dados fica indisponível, o erro é localizado rapidamente.
- Em muitos artigos e livros, também é chamada de **camada de infraestrutura**. O isolamento permite adicionar **novas interfaces sem alterar as funcionalidades**.
- **Backend-to-Frontend**: APIs adaptadas a um consumidor específico, em vez de uma genérica. Por exemplo, três APIs: navegador web, Android e iOS. Veja [[Backend for Frontend (BFF)]].

## Resumo da própria apostila
Sem essas duas camadas, a regra de negócio não pode ser usada. Os **Adaptadores de Interface** organizam e padronizam a execução dos casos de uso (**Controllers**), adequam as respostas ao requisitante (**Presenters**) e dão acesso a dados de fora (**Gateways**). **Frameworks e Drivers** implementa o acesso a dados externos e expõe os casos de uso, muitas vezes com frameworks.

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008)
