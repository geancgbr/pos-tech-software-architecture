---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Documentação, Tipos de documentação]
---

# Documentação de Software

Cada tipo de documentação tem sua função, e juntas elas garantem que o software seja **compreendido e mantido** ao longo do tempo.

## Utilização do projeto
Ajuda os **usuários finais** (e membros do time) a usar o software. Exemplo: **manual do usuário** com as funcionalidades e as tarefas, usando instruções passo a passo, imagens, vídeos e fluxogramas.

## Desenvolvimento do projeto
Voltada ao **time de desenvolvimento**: registra o processo, da concepção à entrega. Inclui tecnologias, decisões de arquitetura e design, testes realizados, bugs encontrados e soluções adotadas.
- Exemplo: documento que descreve a **arquitetura** (cada camada, componentes e comunicação), com diagramas, fluxogramas e especificações técnicas.
- Exemplo: **relatório de testes** (unitários, integração, funcionais, desempenho) com os resultados.

## Infraestrutura
Descreve os componentes e as configurações da infraestrutura de TI (hardware, software, rede), para facilitar manutenção e gerenciamento. É útil para garantir que a configuração do ambiente de desenvolvimento e de produção seja **consistente e adequada**.
- **Inventário de hardware**: servidores, roteadores, switches, firewalls, armazenamento, com modelo, número de série, localização, rede, BIOS/firmware e histórico de manutenção.
- **Inventário de software**: SOs, aplicativos, utilitários, monitoramento, com nome, versão, data de instalação, segurança e licenças.
- **Diagramas de rede**: topologia, conectividade lógica, fluxo de dados.
- **Políticas e procedimentos**: backup, acesso remoto, manutenção preventiva, recuperação de desastres.
- **Documentação de configuração**: IPs, firewall, segurança, armazenamento.
- **Relatórios de monitoramento**: uso de recursos, falhas, alertas.

## Arquitetura do projeto
Descreve a estrutura e o design do software (arquitetura, padrões, componentes, interfaces) para facilitar desenvolvimento, manutenção e evolução, e garantir que ele seja **escalável**.
- **Visão geral**: objetivos de design, requisitos, restrições, decisões importantes.
- **Diagramas de arquitetura**: componentes, interfaces, dependências, fluxos de dados (blocos, sequência, estado...).
- **Padrões de design** usados, com exemplos de onde aparecem.
- **Descrição dos componentes**: objetivos, funcionalidades, interfaces e comunicação.
- **Interfaces do sistema**: APIs, protocolos, formatos de dados.
- **Decisões de design** e os motivos por trás delas.

Ferramentas mostradas no Hands On: **Swagger** e **Redoc**.

Aparece em: [[ARQ 03 - Documentação, testabilidade e modificabilidade]]
