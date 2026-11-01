---
tags: [pos-tech/fase-1, seguranca, indice]
disciplina: Desenvolvimento Seguro
fase: 1
aulas: 6
---

# Desenvolvimento Seguro

[[Fase 1 - Arquitetura de Software]] · Revisão → [[Revisão - Desenvolvimento Seguro]]

## Aulas
| # | Aula | Conceitos-chave |
|---|---|---|
| 1 | [[DS 01 - Vulnerabilidades, ataques e intrusões]] | [[Security by Design]], [[Princípio do Menor Privilégio]], [[Normas e Regulamentações de Segurança]] |
| 2 | [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]] | [[Tipos de Ataques]], [[SQL Injection e Command Injection]], [[XSS (Cross-Site Scripting)]] |
| 3 | [[DS 03 - Bibliotecas de software]] | [[Licenças de Software]], [[Segurança de Bibliotecas de Terceiros]] |
| 4 | [[DS 04 - Análise estática de código]] | [[Manutenibilidade]], [[Análise Estática de Código]], [[SonarQube]] |
| 5 | [[DS 05 - OWASP e OWASP Top 10]] | [[OWASP]], [[OWASP Dependency-Track]], [[OWASP Juice Shop e WebGoat]], [[OWASP Web Security Testing Guide]] |
| 6 | [[DS 06 - Padrões de segurança]] | [[AWS Well-Architected]], [[CIS AWS Foundations Benchmark]], [[PCI DSS]], [[NIST 800-53]], [[ISO 27001 e ISO 27002]] |

## Normas e padrões que aparecem em mais de uma aula
| Norma | Aula 1 | Aula 6 |
|---|---|---|
| [[ISO 27001 e ISO 27002]] | Requisitos do SGSI e controles por categoria | Pontos da 27001 e controles da 27002; "não são exatamente padrões de segurança" |
| [[NIST 800-53]] | Centenas de controles; requisito da FISMA | 5 funções: Identificar, Proteger, Detectar, Responder, Recuperar; Revisão 5 |
| [[PCI DSS]] | Dados de cartão; PCI SSC | Os pontos principais (rede, dados, acesso, monitoramento...) |

## Ferramentas citadas
| Para quê | Ferramenta |
|---|---|
| Vulnerabilidades de dependências | `npm audit`, [[OWASP Dependency-Track]] |
| Análise estática | ESLint, Pylint, RuboCop, Checkstyle, Cppcheck, [[SonarQube]] |
| Encontrar vulnerabilidades | OWASP ZAP |
| Treinamento | [[OWASP Juice Shop e WebGoat\|OWASP Juice Shop, OWASP WebGoat]] |
| Avaliar a nuvem AWS | AWS Well-Architected Tool, Trusted Advisor, AWS Security Hub |

## Lab prático
[ddd-hexagonal](https://github.com/geancgbr/ddd-hexagonal): a API de pedidos ganhou validação de entrada contra SQL Injection e XSS, menor privilégio no banco, rede interna, SBOM com Trivy (vulnerabilidades e licenças), SpotBugs/FindSecBugs, SonarQube e OWASP ZAP, além de um mapa do OWASP Top 10 2021. É código meu para praticar, não conteúdo da apostila.

## Material
PDFs em `~/Desktop/FASE 1/Desenvolvimento Seguro/`. **As notas resumem apenas o conteúdo escrito nos PDFs.** Quatro temas citados nos títulos ou nos resumos **não estão no texto**: a diferença entre ataque, vulnerabilidade e intrusão (aula 1); o buffer overflow e o impacto do XSS na autenticação JWT (aula 2); e a lista do OWASP Top 10 (aula 5). As figuras (como a da UA-Parser-JS) não estão nas notas.

## Referências
AWS · CISA · GAT InfoSec · OSTEC · Varonis · Aiqon · CNET · Innovation & Tech Today · Simplilearn · CISOAdvisor (2021) · EVEO · UFPR · VCX Solutions · DevMedia · Softplan · Tecnisys · OWASP · Borges (2023) · Dahn (Stripe) · IBM
