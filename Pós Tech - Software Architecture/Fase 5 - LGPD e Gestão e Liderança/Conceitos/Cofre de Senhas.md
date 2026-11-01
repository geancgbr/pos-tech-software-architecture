---
tags: [pos-tech/fase-5, lgpd, conceito]
aliases: [Cofre de segredos, Secrets manager, Rotação de credenciais]
---

# Cofre de Senhas

Ferramenta que armazena credenciais ("**segredos**") para que o software **não as guarde**, com **rotação** e troca de credenciais **sem alterar o software** ([[LGPD 06 - LGPD no desenvolvimento de software]]).

- **Pode** gerenciar o acesso (**mínimo privilégio**), **registra** uso e permite renovar ou revogar; em cloud, **pode** rotacionar automaticamente ([[LGPD 06 - LGPD no desenvolvimento de software]]).
- Exemplo: cofre + rotação garante acesso só a quem precisa, **por um tempo curto** ([[LGPD 06 - LGPD no desenvolvimento de software]]).
- **Armazenamento de configurações** (outra ferramenta, usada **junto aos** cofres): guarda dados **não sensíveis** fora do software; permite mudar configurações sob demanda (ex.: desativar um software que vaza dados) e **ambientes segregados** ([[LGPD 06 - LGPD no desenvolvimento de software]]). Na revisão: configurações segregadas, que permitem mudar a configuração de forma remota **ou até mesmo** invalidar um acesso suspeito ([[LGPD 07 - Considerações finais na LGPD]]).
- Na disciplina Estrutura de Microsserviços Parte II, o cofre de senhas aparece como exemplo de gerenciamento de chaves ([[Criptografia e mTLS]]).

Aparece em: [[LGPD 06 - LGPD no desenvolvimento de software]], [[LGPD 07 - Considerações finais na LGPD]]
