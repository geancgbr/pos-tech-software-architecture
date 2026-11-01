---
tags: [pos-tech/fase-5, lgpd, indice]
disciplina: Privacidade de Dados e LGPD
fase: 5
aulas: 7
---

# Privacidade de Dados e LGPD

[[Fase 5 - LGPD e Gestão e Liderança]] · Revisão → [[Revisão - Privacidade de Dados e LGPD]] · Conceito → [[LGPD]]

> [!note] Os PDFs não trazem nome de autor (a aula 1 fala em "docentes"). As aulas 1 a 4 tratam da lei, das bases legais, da governança de dados e da IA; as aulas 5 e 6, da implementação em nuvem e do desenvolvimento de software; a aula 7 revisa tudo.

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[LGPD 01 - Introdução à LGPD e seus princípios básicos]] | [[LGPD]], [[Agentes de Tratamento]], [[Direitos dos Titulares]], artigos para a equipe técnica |
| 2 | [[LGPD 02 - A segurança dos usuários e de seus dados]] | [[Bases Legais da LGPD]] (dez bases, quatro pilares), [[Criptografia e mTLS\|criptografia]], [[Anonimização de Dados]] |
| 3 | [[LGPD 03 - Governança de dados]] | [[Governança de Dados]] (componentes, benefícios, riscos, como criar) |
| 4 | [[LGPD 04 - Inteligência artificial na LGPD]] | [[Inteligência Artificial e LGPD]] (cookies, treinamento, explicabilidade) |
| 5 | [[LGPD 05 - LGPD na implementação da solução de tecnologia]] | [[IaaS, PaaS e SaaS]], [[NIST Cybersecurity Framework]] |
| 6 | [[LGPD 06 - LGPD no desenvolvimento de software]] | [[Privacidade por Design e por Padrão]], [[Cofre de Senhas]], [[Autenticação, Autorização e IAM]], mascaramento |
| 7 | [[LGPD 07 - Considerações finais na LGPD]] | Revisão; encarregado, dados sensíveis, internacionalização |

## Ligações com outras disciplinas
- **Desenvolvimento Seguro (Fase 1)**: a LGPD já aparecia em [[Normas e Regulamentações de Segurança]]; o [[Princípio do Menor Privilégio]] e o [[NIST 800-53]].
- **Estrutura de Microsserviços Parte II (Fase 4)**: [[Criptografia e mTLS]] (at-rest, in-transit, cofre de senhas).
- **Data Engineering (Fase 4)**: o [[DBaaS (Database-as-a-Service)]], aqui como exemplo de PaaS.

## Dúvidas em aberto
- Vigência da lei: 18 de setembro de 2020 (aula 1) × agosto de 2020 (aulas 2, 3 e 4).
- Consentimento como exigência geral (aulas 1, 4 e início da 7) × uma das dez bases legais (aulas 2 e 7).
- Avaliação da criptografia: "mais seguro" e "uma das mais frágeis" (aula 2), "forma inicial... ofuscamento" (aula 6), "um modo seguro" (aula 7).
- Anonimização: identificação "direta ou indireta" (aula 2) × "diretamente" (aula 7).
- Aula 6: o exemplo de criptografia em trânsito é o HTTPS, mas o texto em seguida fala em aplicações em "http".
- Aula 2: "minimização de acesso" descreve reduzir os dados coletados.
- Aula 3: diz que titulares e usuários "representam os controladores e operadores", o que não bate com as definições da aula 1.
- Aula 7: anonimizados fora do escopo da lei, mas "alguns dos dados anonimizados são considerados sensíveis" (art. 5, II); usa "on-transit" em vez de "in-transit".

## Material
PDFs em `~/Downloads/` ("Aula 01- Introdução à LGPD e seus princípios básicos.pdf" a "Aula 07- Considerações finais na LGPD.pdf").
