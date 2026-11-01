---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [NUnit, xUnit, Xunit, MSTest]
---

# Frameworks de Teste .NET (NUnit, xUnit, MSTest)

Frameworks amplamente usados na plataforma .NET para testes de unidade. Os métodos de teste são decorados com **atributos** de cada framework, e as **asserções** comparam o resultado esperado com o real. A principal diferença entre eles está na **sintaxe** e nos **recursos**.

| | NUnit | xUnit | MSTest |
|---|---|---|---|
| `using` | `NUnit.Framework` | `Xunit` | `Microsoft.VisualStudio.TestTools.UnitTesting` |
| Atributo do método | `[Test]` | `[Fact]` | `[TestMethod]` |
| Agrupamento | Classe com `[TestFixture]` | **Sem classe especial**: descoberta de testes mais moderna | Classe com `[TestClass]` |
| Igualdade no exemplo | `Assert.AreEqual(5, result)` | `Assert.Equal(5, result)` | `Assert.AreEqual(5, result)` |
| Extensibilidade | Mais extensível | Mais extensível | Menos opções |

Sobre os asserts, os princípios básicos (verificar igualdade, exceções etc.) são os mesmos nos três, mas a sintaxe pode variar.

O código completo do exemplo `CalculatorTests` está em [[QS 02 - Testes de unidade#Frameworks .NET (C#)]].

Aparece em: [[QS 02 - Testes de unidade]]
