---
tags: [pos-tech/fase-3, monitoramento, datadog, logs, aula]
disciplina: Monitoramento e Acesso Avançado
aula: 3
fonte: "Monitoramento e Acesso Avançado/SOAT - Fase 3 - Monitoramento e acesso avançado - Aula 3_rev2.pdf (Douglas Lima da Silva Martins)"
---

# MAV 03 - Logs com Datadog

← [[MAV 02 - Introdução APM Datadog]] · [[Monitoramento e Acesso Avançado]] · Próxima → [[MAV 04 - Infra com Datadog]]

> [!summary] Em uma frase
> A **ingestão de logs** no **[[Datadog]]**, com **drop rules** e **patterns** para um troubleshooting assertivo. O PDF explica **por que os logs importam**, **8 categorias comuns de severidade** e os **7 tipos principais de logs**. Ver [[Severidade e Tipos de Logs]].

## Hands On
Instrumentar os logs das aplicações que já tinham **APM no Datadog** e analisar os logs enviados. Segundo o resumo, foram aplicadas regras de **drop rule, patterns e usabilidade**, com o **mínimo necessário** para a instrumentação (há requisitos básicos nas aplicações para o envio de logs).

## Por que os logs importam
| Motivo | O que o PDF diz |
|---|---|
| **Rastreamento de atividades** | Histórico detalhado das operações, para entender o comportamento do sistema |
| **Diagnóstico de erros** | Identificar e corrigir falhas, melhorando a confiabilidade |
| **Segurança** | Detectar tentativas de acesso não autorizado e outras vulnerabilidades |
| **Conformidade** | Requisito frequente para cumprir regulamentações e padrões; fundamentais em **investigações forenses** |
| **Desempenho** | Monitorar e identificar **gargalos**; a análise pode melhorar o design e a funcionalidade |
| **Alertas** | Gerar alertas **em tempo real** para eventos críticos |
| **Auditorias** | Ferramenta essencial para auditorias internas e externas; contexto do que aconteceu antes de um incidente |
| **Patterns** | Facilitar os filtros e achar os logs de forma mais ágil (Figura 1) |

## Severidade
O **grau de urgência ou importância** de um evento registrado. Cada nível ajuda a determinar a **urgência e a ação** necessárias (Figura 2).

| Nível | Significado |
|---|---|
| **Debug** | Informações detalhadas, principalmente para devs depurarem |
| **Info** | O **fluxo normal** do aplicativo |
| **Notice** | Eventos **incomuns**, mas não necessariamente errados |
| **Warning** | Algo inesperado aconteceu (ou pode acontecer), mas o aplicativo **ainda funciona** como esperado |
| **Error** | Um **problema sério** na execução, que deve ser investigado e corrigido |
| **Critical** | Um problema **muito sério**, que pode impedir partes do sistema de funcionar |
| **Alert** | Precisa ser corrigido **imediatamente** (ex.: componente indisponível) |
| **Emergency** | Estado crítico: o sistema pode ficar **inutilizável** |

## Os 7 tipos principais de logs
| Tipo | O que registra | Onde encontrar (exemplos do PDF) |
|---|---|---|
| **Sistema** | O SO e seus serviços: inicialização e desligamento, instalação, atualizações, erros de sistema, **eventos de hardware** (falhas de disco, memória, CPU) e **atividades de rede** | **Event Viewer** (Windows), **syslog** (Linux), **Console** (macOS) |
| **Aplicação** | Atividades dentro de um aplicativo: transações de banco, solicitações de rede, operações de usuário, uso de memória e CPU | **Apache**, logs de transação do **MySQL**, logs de eventos do **Microsoft SQL Server** |
| **Segurança** | Tentativas de **login** (bem-sucedidas e fracassadas), alterações de políticas e de direitos de acesso. Detectam atividade suspeita (várias falhas de login) e ajudam em auditorias | **Security Event Log** (Windows), **`/var/log/auth.log`** (Linux), **Console de Segurança** (macOS) |
| **Transação** | Cada operação de transação (inserções, atualizações, exclusões). Garantem **consistência e recuperação** de dados | Bancos de dados |
| **Auditoria** | **Quem fez o quê e quando**: configuração, operações de banco, atividades de usuários. Conformidade com políticas e regulamentos | **Security Audit Log** (SAP), **Audit Log** (WordPress), **Unified Audit Trail** (Oracle) |
| **Eventos** | Eventos significativos: inicialização, instalação, falhas de hardware, alterações de configuração | Event Viewer, syslog e Console, como os de sistema |
| **Erros** | As **falhas** em sistemas ou aplicações: código do erro, data e hora, natureza, **onde ocorreu no código** e o caminho até o ponto de falha | — (o PDF não dá exemplo) |

> Entender a diferença entre os tipos é crucial: cada um serve a um **propósito específico**, com informações para situações distintas.

## Referências
Alura: Confiabilidade... através de logs · AWS: O que são arquivos de log? · Datadog: Modern Log Management & Analytics · Red Hat: O que é o kernel Linux?
