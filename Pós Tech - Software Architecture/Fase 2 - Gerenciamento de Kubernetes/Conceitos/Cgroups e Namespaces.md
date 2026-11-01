---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Cgroups, Namespaces, Kernel Linux, Kernel]
---

# Cgroups e Namespaces

Segundo a aula 1, "junto do Kernel" há duas outras tecnologias que isolam o uso dos contêineres: Cgroups e Namespaces.

**Kernel Linux**: o "núcleo", principal componente do Linux. É a interface central entre o hardware e os processos e gerencia memória, processos, drives, chamadas do sistema e segurança.

| | Cgroups | Namespaces |
|---|---|---|
| Função | **Limites de uso de recursos** dos processos | **Isolamento** transparente e lógico entre contextos |
| Exemplos | Quanto de CPU um processo pode usar; limitar CPU e memória com um comando; controlar quais processos podem ser reiniciados, interrompidos ou congelados | Cada contêiner com seus próprios usuários, rede, disco etc. |
| Efeito no contêiner | Controla os processos, essencial para funcionar **sem gargalos** | Um contêiner "ruim" não afeta os outros |

**Na Fase 3** ([[MON 01 - Introdução ao Zabbix]]): o Docker depende de um ambiente Linux e do **Kernel, Cgroups e Namespaces** para isolar completamente os ambientes com containers; no Windows, a aula instala o Docker pelo **WSL** (subsistema do Windows baseado em Linux).

Aparece em: [[DK 01 - Introdução ao Docker]]
