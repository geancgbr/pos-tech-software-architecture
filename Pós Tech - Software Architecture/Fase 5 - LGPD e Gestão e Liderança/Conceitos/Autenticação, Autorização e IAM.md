---
tags: [pos-tech/fase-5, lgpd, conceito]
aliases: [Autenticação, Autorização, IAM, Identity and Access Management, Gerenciamento de identidade, MFA]
---

# Autenticação, Autorização e IAM

| | **Autenticação** | **Autorização** |
|---|---|---|
| Pergunta | "Você é realmente quem diz ser?" | "O que você está autorizado a fazer aqui?" |
| Como | **Frequentemente** usuário e senha; **múltiplos fatores** em sistemas mais seguros | Permissões a quem já está autenticado |
| Segurança | Cria uma **sessão**, que **pode** ter tempo de vida limitado ou máximo de sessões | Validada **sempre no momento do uso**, não só no login |

Fonte: [[LGPD 06 - LGPD no desenvolvimento de software]].

- **IAM**: identidades criadas, mantidas e excluídas de forma **centralizada e segregada**, como **fonte única** confiável ([[LGPD 06 - LGPD no desenvolvimento de software]]).
- Na aula 2: autenticação garante a identidade (senha, biometria, chave física); autorização limita o acesso conforme necessidade, atuação e responsabilidade ([[LGPD 02 - A segurança dos usuários e de seus dados]]).
- Em PaaS: autorização rigorosa, autenticação robusta e acesso **só necessário** ([[LGPD 05 - LGPD na implementação da solução de tecnologia]]). Na revisão: **centralizar** a validação de identidade ([[LGPD 07 - Considerações finais na LGPD]]).
- Ver [[Princípio do Menor Privilégio]] (Fase 1).

Aparece em: [[LGPD 02 - A segurança dos usuários e de seus dados]], [[LGPD 05 - LGPD na implementação da solução de tecnologia]], [[LGPD 06 - LGPD no desenvolvimento de software]], [[LGPD 07 - Considerações finais na LGPD]]
