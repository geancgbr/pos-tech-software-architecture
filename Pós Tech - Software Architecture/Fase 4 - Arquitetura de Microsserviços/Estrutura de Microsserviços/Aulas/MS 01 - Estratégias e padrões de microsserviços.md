---
tags: [pos-tech/fase-4, microsservicos, aula]
disciplina: Estrutura de Microsserviços
aula: 1
fonte: "Estrutura de Microsserviços/Estrutura de microsserviços - Aula 1.pdf"
---

# MS 01 - Estratégias e padrões de microsserviços

[[Estrutura de Microsserviços]] · Próxima → [[MS 02 - Comunicação entre processos com microsserviços]]

> [!summary] Em uma frase
> A **arquitetura monolítica** (um único executável) é simples enquanto a aplicação é pequena, mas ao crescer derruba o **time-to-market**, a manutenção, a escalabilidade e a confiabilidade. A **[[Arquitetura de Microsserviços]]** decompõe a aplicação em **serviços fracamente acoplados**, cada um com **sua API** e **seu banco** (logicamente), com benefícios e desafios próprios. Os **padrões de microsserviços** se dividem em **3 camadas** e vários **domínios de problemas**.

## Hands On
Começar a refatorar aos poucos a aplicação monolítica fictícia **FIAP Store** (Figura 1) para microsserviços: uma tabela com os **serviços e suas operações** (ex.: **Estoque**: Reservar, Obter e Debitar Estoque) e depois a coluna de **integrações** (ex.: Estoque → **Serviço Notificação**, "Notificar Estoque Baixo"). Há um **link do GitHub** com os materiais.

## Estilo de arquitetura
Define um **conjunto de componentes**, como podem se relacionar e as **regras** de uso. Pode valer para o **sistema inteiro** (monolítica, microsserviços) ou para **um componente** (hexagonal, em camadas). Ver [[Arquitetura Hexagonal]] e [[Arquitetura de Camadas]].

## Arquitetura monolítica
Ver [[Arquitetura Monolítica]].
- A aplicação é **um único componente executável** (ex.: `.exe`, `.war`): todos os módulos rodam **no mesmo processo**, compartilhando **classes e banco de dados**.

**Vantagens (enquanto é pequena)**
| Vantagem | Por quê |
|---|---|
| **Simples de desenvolver** | Um único conjunto de ferramentas |
| **Grandes mudanças fáceis** | Código e schema num único local |
| **Simples de testar** | Teste de ponta a ponta invocando a API ou a tela |
| **Simples de publicar** | Um único artefato copiado para a máquina |
| **Fácil de escalar** | O artefato em várias máquinas com um **balanceador de carga** |

**Desafios (quando cresce)**
- Muitas squads de diferentes frentes de negócio: é preciso **limitar as janelas de publicação** e gastar tempo em **reuniões entre squads**, para nada quebrar o código de outra. Isso **diminui o time-to-market** (o tempo para publicar novas funcionalidades) e a **competitividade**.
- **Autonomia das squads** cada vez mais distante, com todos no **mesmo repositório**; muitos **merges** e quebras para estabilizar a branch da release.
- **Complexidade** crescente: código difícil de entender, correções incompletas.
- **Dia do desenvolvedor mais lento**: carregar tudo na IDE, construir e executar.
- **Escalabilidade**: módulos com necessidades diferentes (RAM, CPU, disco) exigem **grandes máquinas de uso geral**, mais caras.
- **Confiabilidade**: testes mais complexos, mais bugs; uma **exceção não tratada** num módulo pode **derrubar a aplicação inteira**.
- **Stack obsoleta**: difícil de mudar pela incompatibilidade com o código existente.
- Os atributos mais afetados: **manutenção, extensibilidade e testabilidade**.

> [!note] O sentido de "time-to-market" muda no PDF: no monolito, "diminuir o time-to-market" é apresentado como ruim ("ao diminuirmos o time-to-market, diminuímos a nossa competitividade"); nos benefícios dos microsserviços, "reduzir o time-to-market" é apresentado como bom.

## Arquitetura de microsserviços
- **Decompomos funcionalmente** a aplicação num conjunto de **serviços fracamente acoplados**. Um **serviço** é um componente **único e independente**, com funcionalidades de negócio expostas pela **sua própria API**, sem revelar a implementação (classes, tabelas), "criando uma **delimitação de contexto**".
- **Toda comunicação por API**, o que força **cada serviço a ter seu próprio banco** (**logicamente**; não precisa de instância física dedicada). Assim, cada serviço evolui e escala **de forma independente** (Figura 2).

| Benefício | O que o PDF diz |
|---|---|
| **Entrega e deployment contínuos** | Cada serviço tem **seu pipeline de CI/CD**, testes, repositório e publicação **independente**, com **uma única squad** responsável: menor time-to-market |
| **Menor e mais fácil de manter** | Código menor, mais fácil de entender, carregamento mais rápido |
| **Escala independente** | Máquinas otimizadas para o perfil do serviço (ex.: mais RAM, menos CPU, menor custo por GiB) |
| **Isolamento de falhas** | Se um serviço cai, **só ele** fica indisponível |
| **Novas tecnologias** | Tecnologias diferentes por serviço; uma escolha errada é menos impactante |

| Desafio | O que o PDF diz |
|---|---|
| **Decomposição** | Uma decomposição errada gera um **monolito distribuído**, com as desvantagens das **duas** arquiteturas |
| **Sistemas distribuídos** | Comunicação entre processos, **normalmente** pela **rede**: latência, falhas, bloqueios, indisponibilidade; cada serviço deve tratar falhas. Com um banco por serviço, **transações e buscas** entre serviços ficam desafiadoras |
| **Coordenação de publicação** | Funcionalidades com vários serviços exigem publicação **coordenada** entre squads |
| **Quando adotar** | Deve ser **gradual**; tem um **custo de complexidade**. No início, quando a aplicação é pequena, **não há problemas que os microsserviços resolvam**; ao crescer, a decomposição exige uma refatoração não trivial |

## Padrões de arquitetura de microsserviços
Soluções para problemas recorrentes, em **3 camadas**:
- **Padrões de aplicação**: problemas do desenvolvimento de aplicações.
- **Padrões de infraestrutura de aplicação**: infraestrutura que **influencia** o desenvolvimento.
- **Padrões de infraestrutura**: infraestrutura **transparente** para o desenvolvimento.

**Domínios de problemas**
| Domínio | Pergunta |
|---|---|
| **Decomposition** | Como decompor a aplicação em serviços? |
| **Data Patterns** | Como os serviços devem usar banco de dados? |
| **Querying** | Como buscar dados envolvendo vários serviços? |
| **Maintaining data consistency** | Como garantir consistência em transações entre serviços? |
| **Testing** | Como facilitar os testes num ecossistema de várias squads? |
| **UI** | Como montar telas com dados de vários serviços? |
| **Communication style** | Comunicação síncrona ou assíncrona? |
| **Cross-cutting concerns** | Como padronizar as configurações dos serviços? |
| **Security** | Como saber a identidade do cliente? |
| **Reliability** | Como garantir comunicação confiável, mesmo com falhas? |
| **Transactional messaging** | Como enviar mensagens com as atualizações das transações? |
| **Observability** | Como entender o comportamento de vários serviços? |
| **External API** | Como os clientes acessam os serviços? |
| **Deployment** | Como implantar os serviços? |
| **Discovery** | Como o cliente descobre o **IP** de cada instância? |

O PDF remete ao **diagrama original** com as camadas e os padrões.

## Referências
Microsoft Learn: Estilo de arquitetura de microsserviço · Richardson: A pattern language for microservices · Richardson, *Microservices Patterns* (2018)
