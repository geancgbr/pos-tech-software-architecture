---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Desenvolvimento seguro por design, Secure by Design]
---

# Security by Design

**Desenvolvimento seguro por design**: a segurança é ponto fundamental **desde o início** do desenvolvimento e é criada **junto com ele**, em vez de se corrigirem as vulnerabilidades depois.

**Elementos principais**
1. **Avaliação de ameaças** no início do projeto. Exemplo: telas de login e posts de usuários como alvo de SQL Injection e Command Injection.
2. **Minimização da superfície de ataque**: menos funcionalidades expostas a usuários não autorizados.
3. **[[Princípio do Menor Privilégio]]**.
4. **Segmentação de rede**: sistemas isolados, com controle de acesso entre eles. Exemplo: separar as VPCs das APIs das dos bancos, ou usar sub-redes privadas.
5. **Validação e sanitização de dados**: contra injeção de SQL e de código, buffer overflow etc.
6. **Criptografia** dos dados pessoais e sensíveis, em repouso ou em trânsito.
7. **Teste de segurança contínuo**: varreduras e revisões de código durante todo o ciclo, "assim como o [[TDD (Test-Driven Development)|TDD]]".
8. **Educação em segurança** para toda a equipe.

**O que o diferencia**: estar **sempre focado na segurança, do início ao fim**, com análises e rotinas desde as primeiras linhas, num processo "parecido" com o TDD.

Aparece em: [[DS 01 - Vulnerabilidades, ataques e intrusões]]
