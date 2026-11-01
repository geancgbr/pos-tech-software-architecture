---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [SQL Injection, SQLi, Command Injection, Injeção de SQL, Ataques de injeção]
---

# SQL Injection e Command Injection

São **ataques de injeção**:
- **SQL Injection**: injeta **comandos SQL maliciosos** em campos de texto para acessar, modificar ou excluir dados do banco.
- **Command Injection**: injeta **comandos do sistema operacional** em campos de entrada para executá-los no servidor. É especialmente perigoso quando o código executa comandos de prompt ou shell.

**Como se previne, segundo as aulas**
- **Validação e sanitização** de todo input do usuário, para evitar ataques de injeção de SQL e de código ([[Security by Design]]).
- **Avaliação de ameaças** no início do projeto: telas de login e posts de usuários são alvos potenciais de SQL Injection e Command Injection.
- **[[Análise Estática de Código|Análise estática]] de segurança**: identifica vulnerabilidades conhecidas, como injeções de SQL.
- **Input Validation Testing** do [[OWASP Web Security Testing Guide]]: cobre a injeção de SQL.

**Caso clássico: Sony PSN (2011)**. Um app web não validava as entradas, e dados pessoais e financeiros de milhões de usuários foram expostos. A PSN teve de sair do ar. Outros casos citados: Yahoo (2014), Ashley Madison (2015), TalkTalk (2015), Uber (2016), Equifax (2017).

Aparece em: [[DS 01 - Vulnerabilidades, ataques e intrusões]], [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]]
