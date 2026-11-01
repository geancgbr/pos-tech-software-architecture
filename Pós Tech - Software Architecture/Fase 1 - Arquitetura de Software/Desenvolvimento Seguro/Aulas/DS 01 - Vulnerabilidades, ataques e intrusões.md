---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 1
fonte: "Aula 1.pdf"
---

# DS 01 - Vulnerabilidades, ataques e intrusões

[[Desenvolvimento Seguro]] · Próxima → [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]]

> [!summary] Em uma frase
> Software está em todos os pontos vitais da sociedade, e há quem explore suas falhas. Por isso a segurança precisa vir **desde o início** ([[Security by Design]]), apoiada em [[Normas e Regulamentações de Segurança|normas e regulamentações]].

## Hands On (vídeos)
Os temas principais do desenvolvimento seguro: técnicas e boas práticas para quando estamos arquitetando sistemas ou desenvolvendo software.

## Security by Design (desenvolvimento seguro por design)
A segurança é tratada como **ponto fundamental desde o início** do desenvolvimento e é construída junto com ele, em vez de se corrigirem vulnerabilidades depois.

| Elemento | O que é | Exemplo da apostila |
|---|---|---|
| **Avaliação de ameaças** | Identificar as potenciais ameaças **já no início** do projeto. Ataques e cenários são concebidos, preparados e testados em tempo de desenvolvimento | Avaliar páginas que podem ser alvo de SQL Injection ou Command Injection: telas de login, posts com mensagens de usuários |
| **Minimização de superfície de ataque** | Diminuir a exposição, reduzindo as funcionalidades expostas a usuários não autorizados | Sem exemplo na apostila |
| **[[Princípio do Menor Privilégio]]** | Cada usuário tem acesso só ao **mínimo necessário** para sua função. Vale no desenvolvimento e na arquitetura | Quem deve acessar a tela de gerenciamento de usuários? Quanto menos acessos autorizados, mais seguro |
| **Segmentação de rede** | Redes e sistemas o mais isolados possível, com controle de acesso entre eles. Se houver comprometimento, só uma parte é afetada | Separar as VPCs das APIs das dos bancos de dados, ou deixá-las só em sub-redes privadas, sem acesso direto da internet |
| **Validação e sanitização de dados** | Todo input do usuário é validado e sanitizado, para evitar ataques de injeção de SQL e de código, buffer overflow etc. | Sem exemplo na apostila |
| **Criptografia** | Dados pessoais, principalmente os sensíveis, criptografados **em repouso ou em trânsito** | Sem exemplo na apostila |
| **Teste de segurança contínuo** | Assim como no [[TDD (Test-Driven Development)\|TDD]], testes de segurança (varreduras de vulnerabilidades, revisões de código) durante **todo o ciclo** | Sem exemplo na apostila |
| **Educação em segurança** | Toda a equipe treinada em boas práticas de desenvolvimento seguro | Sem exemplo na apostila |

O que diferencia o Security by Design é **estar sempre focado na segurança, do início ao fim do projeto**, com análises e rotinas desde as primeiras linhas, num processo "parecido" com o TDD.

## Normas e regulamentações
- Variam por **indústria** (financeira, saúde), por **país** (LGPD, GDPR) e por requisitos específicos.
- Cumpri-las garante que o software foi construído com segurança e com padrões de segurança cibernética, e também **serve de garantia para os clientes**.

| Norma | O que é, segundo a apostila |
|---|---|
| **ISO/IEC 27001** | Padrão internacional com os requisitos para criar e manter um **SGSI** (Sistema de Gestão de Segurança da Informação). Diretrizes e controles para proteger informações, minimizar riscos, gerenciar incidentes e garantir conformidade |
| **ISO/IEC 27002** | **Complemento** da 27001, com um conjunto maior de controles divididos em categorias |
| **NIST SP 800-53** | Do Instituto Nacional de Padrões e Tecnologia dos EUA. Centenas de controles (acesso, autenticação, auditoria e monitoramento, criptografia, incidentes...). Muito usado no governo dos EUA e por quem negocia com ele, porque é requisito para conformidade com a **FISMA** |
| **GDPR** | Regulamento da **União Europeia** para proteção de dados pessoais dos cidadãos da UE: consentimento do titular, direitos dos indivíduos etc. |
| **LGPD** | Lei brasileira, fortemente inspirada na GDPR, que regulamenta a proteção de dados pessoais dos cidadãos brasileiros |
| **HIPAA** | Lei dos EUA de **1996** que protege a privacidade e a segurança dos dados de **saúde**. Também trata da portabilidade do seguro saúde e da padronização das transações de informações de saúde. Componentes: regras de privacidade, de segurança, de notificação de violação e de aplicação e fiscalização |
| **PCI DSS** | Padrões de segurança para proteger os dados de **processamento de cartão de crédito**. Iniciativa do PCI SSC (Visa, MasterCard, American Express, Discover, JCB) |
| **Resolução Bacen nº 4.553/2017** | Do **Banco Central do Brasil**: diretrizes de segurança cibernética no **setor financeiro**, para garantir integridade, confidencialidade e disponibilidade |
| **SOC 2** | **Relatório de auditoria** que avalia os controles de segurança em um ambiente de serviços de TI |

> [!important] Qual seguir?
> Não é preciso seguir todas, o que seria quase impossível. Use alguma como **base**, como a ISO 27001 e 27002 (padrões internacionais) ou a que regula seu mercado (HIPAA, Bacen). **LGPD e GDPR não são sugestões: são leis e devem ser seguidas.**

Detalhes em [[Normas e Regulamentações de Segurança]].

> [!note] O resumo final do PDF cita "a diferença entre ataque, vulnerabilidade e intrusões", mas o texto do PDF não define esses termos.

## Referências
AWS, *ISO/IEC 27001* e *Security by Design* · CISA, *Security by Design* · GAT InfoSec (guia de Security by Design) · OSTEC, *ISO 27002* (2016) · Varonis, *NIST 800-53* (2023)
