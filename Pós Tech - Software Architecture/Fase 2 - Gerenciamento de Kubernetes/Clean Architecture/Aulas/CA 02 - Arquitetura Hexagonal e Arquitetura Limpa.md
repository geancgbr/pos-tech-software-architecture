---
tags: [pos-tech/fase-2, clean-architecture, aula]
disciplina: Clean Architecture
aula: 2
fonte: "Aula 2.pdf (Erick Muller)"
---

# CA 02 - Arquitetura Hexagonal e Arquitetura Limpa

← [[CA 01 - Introdução e SOLID]] · [[Clean Architecture]] · Próxima → [[CA 03 - Camada de entidades]]

> [!summary] Em uma frase
> Os dois diagramas mais usados como base são o da **[[Arquitetura Hexagonal]]** e o do livro **"Arquitetura Limpa"**. **Não são a mesma coisa**, mas compartilham ideias: no centro, **Entidades** e **Casos de Uso** (as regras de negócio); por fora, **Portas e Adaptadores** para falar com o mundo exterior.

## Hands On (vídeos)
Os componentes da Arquitetura Hexagonal e da Limpa: o papel das entidades, como a separação de responsabilidades é reforçada em cada camada e os pontos em comum entre as duas.

## Entidades (Entity), no centro
- O diagrama da aula (Figura 1, fonte: reflectoring.io) é de uma aplicação de Arquitetura Hexagonal. A primeira ideia compartilhada com a Limpa é que **no centro fica a camada de Entidades**.
- Entidades são os **elementos de negócio**: uma "Venda", um(a) "Aluno(a)", uma "Ordem de Pagamento". Modelam os atores de um campo de conhecimento, **na abstração necessária para o software**, e não como reflexo direto da vida real.
- A camada guarda os dados **e as regras e restrições** de cada elemento (consistência): não existe "Matrícula" sem "Estudante", nem "Venda" sem "Cliente".
- Pelo SOLID, cada elemento implementa só o necessário. Conceitos simples também podem ser isolados como entidades, e entidades podem compor outras: uma "Movimentação Financeira" tem "Conta Origem", "Conta Destino" (ambas do tipo "Conta") e "Valor".
- Os nomes seguem a **[[Linguagem Ubíqua|linguagem ubíqua]]** do *Domain-Driven Design* (Eric Evans): a linguagem do **negócio e do cliente**, não a da implementação (TypeScript, C#, Java...).
- Esse isolamento torna a regra **testável**: dá para testar o núcleo, a validação de campos e as dependências entre elementos.

Exemplo da aula, em TypeScript:
```typescript
class CNPJ {
  value: string;
  constructor(cnpj: string) {
    if (!CNPJ.validar(cnpj)) {
      throw new Error("CNPJ invalido");
    }
    this.value = cnpj;
  }
  static validar(valor: string): boolean {
    // validar o cnpj
    return true;
  }
}

class CPF {
  value: string;
  constructor(cpf: string) {
    if (!CPF.validar(cpf)) {
      throw new Error("CPF invalido");
    }
    this.value = cpf;
  }
  static validar(valor: string): boolean {
    // validar o cpf
    return true;
  }
}

type Pessoa = {
  nome: string;
}

type PessoaFisica = Pessoa & {
  nascimento: Date;
  cpf: CPF;
}

type PessoaJuridica = Pessoa & {
  cnpj: CNPJ;
  data_abertura: Date;
}
```
"Pessoa" se especializa em "PessoaFisica" e "PessoaJuridica", com tipos nativos (string, Date) e classes próprias (CPF, CNPJ) que validam o valor.

## Casos de Uso
- É onde ficam as **regras de negócio**: um a um, os casos de uso identificados na análise, e as regras complexas que **coordenam várias entidades**. Ficam fora da camada de Entidades e **desconectados** da interface com o mundo exterior.
- Um caso de uso **só pode usar outros casos de uso ou componentes da camada de Entidades**. Pode ser organizado em pacotes, mas as regras de acesso se mantêm.
- Até aqui não se fala de armazenamento nem de rotas de API. Tudo o que não é regra de negócio é **externo** e fica em camadas de fora.

```typescript
class CadastrarClientePessoaFisicaUseCase {
  /* recebe os dados de uma pessoa fisica, verifica se estao corretos */
  pessoaFisica: PessoaFisica;
  constructor(nome: string, cpf: string, nascimento: Date) {
    this.pessoaFisica.nome = nome;
    this.pessoaFisica.nascimento = nascimento;
    this.pessoaFisica.cpf = new CPF(cpf);
  }
}
```
O caso de uso recebe os dados, cria a PessoaFisica, valida e, se estiver tudo certo, adiciona ao Repositório. Outro exemplo: "Efetuar Movimentação Financeira".

## Portas e Adaptadores (Arquitetura Hexagonal)
- As interfaces de comunicação atendem duas necessidades: **trafegar dados de forma padronizada** e **atender bem às requisições**. A analogia é uma **porta USB**, que tem padrões do plugue até a troca lógica de dados.
- **Ports**: **Input Port** informa os dados de que o caso de uso precisa; **Output Port** define como as respostas são entregues.
- **Adapters**: adaptam interfaces e dados para falar com um elemento externo (banco de dados, API, o barramento de API do próprio software). Isolam e abstraem esse elemento para as camadas internas. Exemplo: um dado do banco que precisa ir em JSON para a Input Port é convertido pelo Adapter.

## E a Arquitetura Limpa?
A primeira das diferenças fundamentais: as camadas **externas aos casos de uso são duas**:
1. uma com os componentes de **interface e adaptadores**, que ligam o mundo exterior ao núcleo;
2. uma **mais externa**, que implementa as interfaces com o mundo exterior (bancos de dados, APIs).

Pelo resumo da aula, a Arquitetura Limpa tem **mais elementos e mais regras**, e **só as camadas exteriores podem instanciar elementos das camadas interiores**.

## Referências
Evans, *Domain-Driven Design* (2003) · Martin, *Arquitetura Limpa* (2019) · Martin, *Clean Code* (2008)
