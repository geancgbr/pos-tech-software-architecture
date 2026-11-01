---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Arquitetura em camadas do DDD, Layered Architecture]
---

# Camadas do DDD

Evans organiza a arquitetura em **4 camadas**:

| Camada | Responsabilidade | Não faz | Exemplo na escola |
|---|---|---|---|
| **Interface de Usuário** | GUI, CLI, APIs para outros sistemas | Não se aplica | Não há exemplo na apostila |
| **Aplicação** | Faz a mediação entre UI e Domínio, organiza as tarefas, dispara rotinas e reporta mudanças | **Não tem regra de negócio** e não altera o estado dos objetos | Rotina diária que contabiliza faltas e devolve o resultado |
| **Domínio** | O **"coração do software"**: regras de negócio, mudanças de estado, criação de registros | **Não armazena** dados: entrega para a Infraestrutura | Cálculo da nota com desconto por atraso |
| **Infraestrutura** | Suporte técnico: persistência, mensageria, padrão de interação entre camadas (quando não há integração direta) | Não se aplica | Não há exemplo na apostila |

Em algumas arquiteturas, a camada de Aplicação é fundida com a de Interface.

> [!warning] Na disciplina Arquitetura de Software, a camada de aplicação **contém** a lógica de negócios. Veja a comparação em [[Arquitetura de Camadas]].

Aparece em: [[DDD 05 - Implementando arquitetura e lógica]]
