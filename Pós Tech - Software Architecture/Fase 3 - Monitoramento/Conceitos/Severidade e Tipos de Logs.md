---
tags: [pos-tech/fase-3, monitoramento, logs, conceito]
aliases: [Severidade dos logs, Tipos de logs, Log severity]
---

# Severidade e Tipos de Logs

## Severidade
O **grau de urgência ou importância** de um evento registrado ([[MAV 03 - Logs com Datadog]]):
8 categorias comuns, segundo o PDF: **Debug** (depuração) · **Info** (fluxo normal) · **Notice** (incomum, não necessariamente errado) · **Warning** (algo inesperado, mas ainda funciona) · **Error** (problema sério a investigar) · **Critical** (pode impedir partes do sistema) · **Alert** (corrigir imediatamente) · **Emergency** (o sistema pode ficar inutilizável).

## Os 7 tipos principais
| Tipo | O que registra | Exemplos de onde encontrar |
|---|---|---|
| **Sistema** | O SO e seus serviços, hardware, rede | Event Viewer, syslog, Console (macOS) |
| **Aplicação** | Atividades de um aplicativo | Apache, MySQL, Microsoft SQL Server |
| **Segurança** | Logins, políticas, direitos de acesso | Security Event Log, `/var/log/auth.log`, Console de Segurança |
| **Transação** | Inserções, atualizações, exclusões | Bancos de dados |
| **Auditoria** | Quem fez o quê e quando | SAP, WordPress, Oracle |
| **Eventos** | Inicialização, instalação, falhas, configuração | Event Viewer, syslog, Console |
| **Erros** | As falhas, com código, data, natureza e local no código | — |

- No New Relic, o **Log Summary** mostra os logs de severidade **Error ou pior** ([[MAV 08 - Logs com New Relic]]).

Aparece em: [[MAV 03 - Logs com Datadog]]
