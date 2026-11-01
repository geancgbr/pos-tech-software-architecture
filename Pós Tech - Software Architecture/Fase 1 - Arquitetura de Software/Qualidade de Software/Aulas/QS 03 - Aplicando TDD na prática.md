---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 3
fonte: "Aula 03 - Aplicando TDD na prática.pdf"
---

# QS 03 - Aplicando TDD na prática

← [[QS 02 - Testes de unidade]] · [[Qualidade de Software]] · Próxima → [[QS 04 - Testes de integração]]

> [!summary] Em uma frase
> O [[TDD (Test-Driven Development)|TDD]] é uma metodologia em que se escrevem **testes automatizados antes do código**, num ciclo de três etapas: **Red → Green → Refactor**.

## Hands On (vídeo)
TDD aplicado a uma nova funcionalidade: primeiro o teste que descreve o comportamento esperado, depois ver as falhas, implementar o código e, em seguida, refatorar.

## O ciclo Red-Green-Refactor
O fluxo está desenhado na Figura 1 do PDF (fonte: Alves, 2013).

| Etapa | O que se faz | No exemplo `IsAlphaString` |
|---|---|---|
| 🔴 **Red** (Vermelho) | Escreve-se um teste automatizado **para falhar**, descrevendo o comportamento esperado **antes** de implementar | O teste espera que `"Hello"` seja válido, mas a funcionalidade ainda não foi implementada |
| 🟢 **Green** (Verde) | Implementa-se o **código mínimo** para o teste passar | Um `foreach` que retorna `false` ao achar um caractere que não é letra |
| 🔵 **Refactor** (Refatoração) | Melhora-se a qualidade e a legibilidade **sem mudar o comportamento**, e **roda-se o teste de novo** | Troca o `foreach` por LINQ: `input.All(c => char.IsLetter(c))` |

```csharp
// RED: o teste vem primeiro
using NUnit.Framework;

[TestFixture]
public class StringValidatorTests
{
    [Test]
    public void IsAlphaString_ShouldReturnTrueForAlphaString()
    {
        // Arrange
        StringValidator validator = new StringValidator();
        // Act
        bool result = validator.IsAlphaString("Hello");
        // Assert
        Assert.IsTrue(result);
    }
}
```

```csharp
// GREEN: o código mínimo para passar
public class StringValidator
{
    public bool IsAlphaString(string input)
    {
        foreach (char c in input)
        {
            if (!char.IsLetter(c))
            {
                return false;
            }
        }
        return true;
    }
}
```

```csharp
// REFACTOR: mais conciso com LINQ, mesmo comportamento
public class StringValidator
{
    public bool IsAlphaString(string input)
    {
        return input.All(c => char.IsLetter(c));
    }
}
```

## Pontos-chave
- A refatoração melhora o código sem afetar o comportamento esperado, deixando-o mais legível, manutenível e confiável.
- Em cenários mais complexos, com mais casos de teste, o fluxo é **o mesmo** (Red → Green → Refactor). Ele garante o mínimo de cobertura, permite validar diferentes cenários e refinar continuamente o código.
- **Benefícios do TDD** (resumo da apostila): maior confiabilidade do código, menor quantidade de defeitos e maior capacidade de refatoração.

## Referências
Alves, *TDD – Test-Driven Development* (2013) · Aniche, *Test-Driven Development: Teste e Design no Mundo Real* (Casa do Código, 2012)
