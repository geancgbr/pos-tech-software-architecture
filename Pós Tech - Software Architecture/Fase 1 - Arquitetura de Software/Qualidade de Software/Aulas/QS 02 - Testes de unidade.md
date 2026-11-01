---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 2
fonte: "Aula 02 - Testes de unidade.pdf"
---

# QS 02 - Testes de unidade

← [[QS 01 - Principais conceitos]] · [[Qualidade de Software]] · Próxima → [[QS 03 - Aplicando TDD na prática]]

> [!summary] Em uma frase
> O [[Teste de Unidade|teste de unidade]] verifica, de forma **isolada**, se cada unidade do código (função, método, classe ou trecho) funciona corretamente. Na plataforma .NET, os frameworks são [[Frameworks de Teste .NET (NUnit, xUnit, MSTest)|NUnit, xUnit e MSTest]].

## Hands On (vídeo)
Criação de testes de unidade num projeto que estava com **baixa cobertura de testes**, enfatizando a importância de testar desde o início do projeto.

## O que é
- Verifica o funcionamento de **uma unidade** do código-fonte: funções, métodos, classes ou pequenos trechos de código.
- **Objetivo**: garantir que cada unidade funcione corretamente **de forma isolada**, antes de ser integrada a módulos maiores ou ao sistema.

## Benefícios
| Benefício | Por quê |
|---|---|
| **Detecção precoce de defeitos** | Testar de forma isolada encontra erros e falhas de lógica cedo, quando é mais fácil e rápido corrigir. Reduz custo e aumenta a eficiência |
| **Facilita a manutenção** | Dá segurança para alterar o código: verifica rapidamente se a mudança causou problema em outras partes |
| **Documentação viva** | Exemplos claros de como cada unidade deve ser usada e se comportar. Ajuda outros devs, mesmo com alta rotatividade de equipe |
| **Confiança e qualidade** | Testes abrangentes aumentam a confiança na estabilidade, e o usuário final tem uma experiência mais consistente |

## Boas práticas (guidelines)
1. **Escreva os testes antes do código** ([[TDD (Test-Driven Development)|TDD]]): ajuda a definir requisitos e comportamentos e garante cobertura adequada.
2. **Mantenha os testes pequenos e rápidos**: divida em unidades lógicas menores e evite testar funcionalidades complexas num único teste.
3. **Cobertura abrangente**: todos os caminhos e condições, incluindo diferentes entradas, **casos de borda** e **cenários de erro**.
4. **Automatize**: use frameworks de teste, integrando-os ao build e à **integração contínua**.
5. **Teste o comportamento esperado e o não esperado**: também os casos em que o código deve falhar.
6. **Atualize os testes conforme o código evolui**.

Os testes de unidade devem ser feitos **junto com outras formas de teste** (integração, sistema) para uma cobertura completa.

## Frameworks .NET (C#)
O mesmo teste, `CalculatorTests.Add_ShouldReturnCorrectSum`, nos três frameworks. Todos seguem a estrutura **Arrange / Act / Assert**:

```csharp
// NUnit
using NUnit.Framework;

[TestFixture]
public class CalculatorTests
{
    [Test]
    public void Add_ShouldReturnCorrectSum()
    {
        // Arrange
        Calculator calculator = new Calculator();
        // Act
        int result = calculator.Add(2, 3);
        // Assert
        Assert.AreEqual(5, result);
    }
}
```

```csharp
// xUnit
using Xunit;

public class CalculatorTests
{
    [Fact]
    public void Add_ShouldReturnCorrectSum()
    {
        // Arrange
        Calculator calculator = new Calculator();
        // Act
        int result = calculator.Add(2, 3);
        // Assert
        Assert.Equal(5, result);
    }
}
```

```csharp
// MSTest
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class CalculatorTests
{
    [TestMethod]
    public void Add_ShouldReturnCorrectSum()
    {
        // Arrange
        Calculator calculator = new Calculator();
        // Act
        int result = calculator.Add(2, 3);
        // Assert
        Assert.AreEqual(5, result);
    }
}
```

A principal diferença está na **sintaxe** e nos **recursos**:

| | NUnit | xUnit | MSTest |
|---|---|---|---|
| Atributo do método de teste | `[Test]` | `[Fact]` | `[TestMethod]` |
| Classe de teste | Específica, com `[TestFixture]` | **Sem** classe especial (descoberta de testes mais moderna) | Específica, com `[TestClass]` |
| Assert de igualdade no exemplo | `Assert.AreEqual` | `Assert.Equal` | `Assert.AreEqual` |
| Extensibilidade | **Mais** extensível | **Mais** extensível | **Menos** opções |

Detalhes em [[Frameworks de Teste .NET (NUnit, xUnit, MSTest)]].

> [!note] O resumo final do PDF diz que a aula apresentou "maneiras para criar mock", mas o texto do PDF não detalha esse conteúdo.

## Referência
Microsoft, *Noções básicas de teste de unidade* (2023)
