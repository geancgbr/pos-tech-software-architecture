---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Menor privilégio, Least Privilege, Acesso mínimo necessário]
---

# Princípio do Menor Privilégio

Cada usuário tem acesso **apenas ao mínimo necessário** para executar sua função no sistema, o que evita riscos desnecessários. Vale **no desenvolvimento e nas features de arquitetura**.

Exemplo da aula 1: quais tipos de usuário devem acessar a tela de gerenciamento de usuários? **Quanto menor o número de acessos autorizados, mais seguro.**

Também aparece no [[PCI DSS]] como "restringir o acesso com base no princípio do acesso mínimo necessário".

## Na disciplina Privacidade de Dados e LGPD (Fase 5)
- Em PaaS, funcionários e pessoas do provedor devem ter **apenas o acesso necessário** ([[LGPD 05 - LGPD na implementação da solução de tecnologia]]).
- Os cofres de senha permitem uma política de **"mínimo privilégio"** ([[Cofre de Senhas]]) ([[LGPD 06 - LGPD no desenvolvimento de software]]).
- O controle de acesso entrega só o conjunto necessário (**minimização do acesso**) ([[LGPD 07 - Considerações finais na LGPD]]).

Aparece em: [[DS 01 - Vulnerabilidades, ataques e intrusões]], [[DS 06 - Padrões de segurança]], [[LGPD 05 - LGPD na implementação da solução de tecnologia]], [[LGPD 06 - LGPD no desenvolvimento de software]], [[LGPD 07 - Considerações finais na LGPD]]
