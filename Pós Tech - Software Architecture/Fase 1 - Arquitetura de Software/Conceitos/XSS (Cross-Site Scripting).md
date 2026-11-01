---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [XSS, Cross-Site Scripting]
---

# XSS (Cross-Site Scripting)

Ataque a **aplicativos web no servidor**: scripts maliciosos são **injetados em páginas web** para acessar os **cookies** de usuários legítimos. Com isso, o atacante obtém acesso ao usuário.

- Segundo o resumo final da aula 2, a aula abordou como o XSS pode impactar a **autenticação JWT**, mas o texto do PDF não detalha isso.
- É detectável pela **[[Análise Estática de Código|análise estática]] de segurança** e coberto pelo **Input Validation Testing** do [[OWASP Web Security Testing Guide]]. É uma das categorias de lição do **WebGoat** ([[OWASP Juice Shop e WebGoat]]).

**Caso clássico: MySpace (2005)**. Samy Kamkar injetou JavaScript no próprio perfil. Quem visitava recebia o script e virava amigo dele. Em horas, centenas de milhares de perfis foram afetados, e o MySpace saiu do ar temporariamente.

Outros casos citados: Twitter (2010), Sony Pictures (2014), eBay (2014), WhatsApp Web (2015), BBC (2015), Yahoo Finance (2017).

Aparece em: [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]]
