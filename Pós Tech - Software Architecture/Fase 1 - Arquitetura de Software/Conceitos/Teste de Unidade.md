---
tags: [pos-tech/fase-1, qualidade, conceito]
aliases: [Testes de unidade, Teste unitário, Testes unitários, Unit Test]
---

# Teste de Unidade

Teste que verifica o funcionamento de **uma unidade do código-fonte** (função, método, classe ou pequeno trecho) **de forma isolada**, antes de integrá-la a módulos maiores ou ao sistema.

**Benefícios**: detecção precoce de defeitos · facilita a manutenção · **documentação viva** do código · confiança e qualidade.

**Boas práticas**
1. Escreva os testes **antes do código** ([[TDD (Test-Driven Development)|TDD]]).
2. Testes **pequenos e rápidos**, sem funcionalidades complexas num único teste.
3. **Cobertura abrangente**: caminhos, condições, entradas diferentes, **casos de borda**, **cenários de erro**.
4. **Automatize** com frameworks, integrando ao build e à integração contínua.
5. Teste o comportamento **esperado e o não esperado** (quando o código deve falhar).
6. **Atualize** os testes conforme o código evolui.

Deve ser combinado com outras formas de teste ([[Teste de Integração|integração]], sistema) para uma cobertura completa.

**Estrutura dos exemplos**: Arrange / Act / Assert. Frameworks .NET: [[Frameworks de Teste .NET (NUnit, xUnit, MSTest)]].

Aparece em: [[QS 02 - Testes de unidade]]
