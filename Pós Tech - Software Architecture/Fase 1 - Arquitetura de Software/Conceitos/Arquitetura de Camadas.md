---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Arquitetura em camadas, Layered Architecture, Camadas]
---

# Arquitetura de Camadas

Padrão arquitetural comum: o sistema é dividido em **camadas** (níveis lógicos), cada uma com sua responsabilidade. As camadas ficam numa **pilha**: as **mais baixas fornecem serviços** e as **mais altas usam esses serviços**.

| # | Camada | Responsabilidade |
|---|---|---|
| 1 | **Apresentação / interface do usuário** | Interação com o usuário: apresenta informações e recebe comandos |
| 2 | **Aplicação** | Contém a **lógica de negócios**, implementando a funcionalidade do domínio do problema |
| 3 | **Persistência de dados** | Leitura e gravação em bancos de dados ou outros armazenamentos |

Algumas implementações acrescentam uma camada de **serviços** ou de **infraestrutura**.

**Objetivo**: separar as preocupações em níveis de abstração, para que cada camada seja implementada, testada e mantida de forma independente. Isso facilita escalabilidade, teste e manutenção e melhora modularidade e flexibilidade.

> [!warning] O termo "Aplicação" muda de sentido entre as apostilas
> - **Arquitetura de Software, aula 1**: a camada de aplicação **contém a lógica de negócios**.
> - **DDD, aula 5** ([[Camadas do DDD]]): a camada de aplicação **não contém lógica de negócio**; as regras ficam na camada de Domínio.
> - **Arquitetura de Software, aula 5** ([[Arquitetura Hexagonal]]): o "Application" do centro do hexágono **não tem relação** com a camada Application da arquitetura de camadas; ele é o core, o domínio.

Aparece em: [[ARQ 01 - Introdução à arquitetura de software]]
