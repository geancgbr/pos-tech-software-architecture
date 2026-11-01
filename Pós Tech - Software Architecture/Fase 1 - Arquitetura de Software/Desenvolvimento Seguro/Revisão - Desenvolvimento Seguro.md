---
tags: [pos-tech/fase-1, seguranca, revisao]
disciplina: Desenvolvimento Seguro
---

# Revisão - Desenvolvimento Seguro

[[Desenvolvimento Seguro]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Security by Design e normas
> [!question]- O que é Security by Design?
> É o desenvolvimento seguro por design: a segurança é ponto fundamental desde o início e é construída junto com o desenvolvimento, em vez de se corrigirem as vulnerabilidades depois. → [[Security by Design]]

> [!question]- Quais são os elementos do Security by Design?
> Avaliação de ameaças, minimização da superfície de ataque, princípio do menor privilégio, segmentação de rede, validação e sanitização de dados, criptografia, teste de segurança contínuo e educação em segurança.

> [!question]- O que é o princípio do menor privilégio?
> Cada usuário tem acesso só ao mínimo necessário para sua função. Quanto menos acessos autorizados, mais seguro. → [[Princípio do Menor Privilégio]]

> [!question]- Qual é o exemplo de segmentação de rede da apostila?
> Separar as VPCs das APIs das dos bancos de dados, ou deixá-las só em sub-redes privadas, sem acesso direto da internet.

> [!question]- A que processo o teste de segurança contínuo é comparado?
> Ao TDD: testes de segurança (varreduras de vulnerabilidades, revisões de código) durante todo o ciclo de desenvolvimento.

> [!question]- ISO 27001 × ISO 27002?
> A 27001 estabelece os requisitos para criar e manter um SGSI. A 27002 é um complemento, com um conjunto maior de controles por categoria. → [[ISO 27001 e ISO 27002]]

> [!question]- Para que serve a NIST SP 800-53, e por que é tão usada nos EUA?
> Fornece diretrizes e centenas de controles de segurança da informação. É muito usada no governo dos EUA e por quem negocia com ele, porque é requisito para conformidade com a FISMA. → [[NIST 800-53]]

> [!question]- GDPR × LGPD?
> GDPR: regulamento da União Europeia para dados pessoais dos cidadãos da UE. LGPD: lei brasileira, fortemente inspirada na GDPR, para dados pessoais dos cidadãos brasileiros. → [[Normas e Regulamentações de Segurança]]

> [!question]- O que é a HIPAA?
> Uma lei dos EUA de 1996 que protege a privacidade e a segurança dos dados de saúde. Também trata da portabilidade do seguro saúde e da padronização das transações de informações de saúde.

> [!question]- Qual regulamentação brasileira trata da segurança cibernética no setor financeiro?
> A Resolução Bacen nº 4.553/2017.

> [!question]- O que é o SOC 2?
> Um relatório de auditoria que avalia os controles de segurança num ambiente de serviços de TI.

> [!question]- É preciso seguir todas as normas?
> Não, seria quase impossível. Use alguma como base (ISO 27001/27002, ou a do seu mercado, como HIPAA e Bacen). LGPD e GDPR são leis e devem ser seguidas.

## Aula 2 - Ataques
> [!question]- Quais são as 7 categorias de ataque a servidores?
> Injeção, negociação de sessão, autenticação, negação de serviço, protocolos e camadas de rede, aplicativos web no servidor e escuta de rede. → [[Tipos de Ataques]]

> [!question]- SQL Injection × Command Injection?
> SQL Injection: injeta comandos SQL em campos de texto para acessar, modificar ou excluir dados do banco. Command Injection: injeta comandos do sistema operacional para executá-los no servidor, o que é perigoso quando o código executa prompt ou shell. → [[SQL Injection e Command Injection]]

> [!question]- Como funciona o ataque Man-in-the-Middle?
> O atacante se posiciona entre a comunicação de duas partes, interceptando ou manipulando as informações sem que elas saibam, para obter senhas, cartões etc.

> [!question]- O que é um ataque de sessão fixa?
> O atacante fixa uma sessão de autenticação válida e força um usuário legítimo a adotá-la, explorando falhas na geração de identificadores de sessão.

> [!question]- DoS × DDoS?
> Os dois sobrecarregam servidor ou rede para derrubar o serviço. O DoS parte de um único ponto. O DDoS usa uma rede de computadores zumbis, atacando de vários lugares.

> [!question]- O que é envenenamento de ARP?
> Comprometer a tabela do ARP (que associa IPs a endereços MAC em redes Ethernet), redirecionando o tráfego para um servidor malicioso.

> [!question]- O que é XSS, segundo a apostila?
> A injeção de scripts maliciosos em páginas web para acessar os cookies de usuários legítimos e, assim, obter acesso ao usuário. → [[XSS (Cross-Site Scripting)]]

> [!question]- Qual foi o ataque famoso à Sony PSN, e o que causou?
> SQL Injection, em 2011: um app web não validava as entradas. Dados pessoais e financeiros de milhões de usuários foram expostos, a PSN saiu do ar e a Sony perdeu reputação.

> [!question]- Qual foi o ataque famoso ao MySpace?
> XSS, em 2005, por Samy Kamkar. Um script no perfil dele fazia quem o visitasse receber o script e virar seu amigo. Centenas de milhares de perfis foram afetados em horas.

## Aula 3 - Bibliotecas
> [!question]- Por que a licença das bibliotecas importa?
> Por compatibilidade com a licença do projeto, por responsabilidade legal (não violar direitos de terceiros) e por liberdade de uso. Ela determina como a biblioteca pode ser usada, modificada e distribuída. → [[Licenças de Software]]

> [!question]- O que a licença MIT exige?
> Permite usar, modificar e distribuir, desde que o aviso de direitos autorais e a licença original sejam mantidos.

> [!question]- O que a licença Apache acrescenta em relação à MIT?
> Disposições específicas para proteger os contribuintes de responsabilidade legal.

> [!question]- Por que a GPL pode afetar a licença do seu projeto?
> Porque exige que o software derivado também seja distribuído sob os termos da GPL.

> [!question]- O que aconteceu com a UA-Parser-JS?
> Três versões dessa biblioteca NPM (cerca de 24 milhões de downloads no mês) foram contaminadas com código para minerar a criptomoeda Monero. → [[Segurança de Bibliotecas de Terceiros]]

> [!question]- O que é cryptojacking?
> Usar o processamento (CPU, GPU) de máquinas alheias para minerar criptomoedas sem o consentimento ou o conhecimento do dono, o que costuma causar lentidão e sobrecarga.

> [!question]- Como garantir que uma biblioteca é segura?
> Fontes confiáveis, bibliotecas populares (mais revisões), auditorias de código, testes de segurança regulares, acompanhamento de vulnerabilidades (`npm audit`), bibliotecas atualizadas e análise estática de código.

## Aula 4 - Análise estática
> [!question]- O que é manutenibilidade, segundo a aula 4?
> A capacidade de o código-fonte ser facilmente compreendido, modificado, corrigido e estendido ao longo do tempo. → [[Manutenibilidade]]

> [!question]- Cite práticas de manutenibilidade.
> Clareza e legibilidade, modularização, testes unitários, gerenciamento de dependências, padrões de codificação, refatoração e documentação adequada.

> [!question]- O que é análise estática de código, e em que difere dos testes dinâmicos?
> É um processo automatizado que examina o código sem executá-lo. Os testes dinâmicos executam e testam o código em tempo real; a análise estática avalia o código em repouso, antes de ele rodar. → [[Análise Estática de Código]]

> [!question]- Quais são as abordagens da análise estática?
> Léxica e sintática, fluxo de controle, dependências, segurança e estilo de código.

> [!question]- Associe cada ferramenta à sua linguagem: ESLint, Pylint, RuboCop, Checkstyle, Cppcheck.
> JavaScript, Python, Ruby, Java e C/C++, respectivamente.

> [!question]- Qual é o grande destaque do SonarQube?
> A capacidade de fornecer uma visão abrangente e detalhada da qualidade do código-fonte. Além disso, ele suporta várias linguagens e é altamente integrável a CI/CD. → [[SonarQube]]

## Aula 5 - OWASP
> [!question]- O que é o OWASP, e qual é o principal projeto dele?
> A organização que promove práticas de segurança de software e melhora a segurança de aplicações web no mundo. O principal projeto é o OWASP Top 10. → [[OWASP]]

> [!question]- Como funciona o OWASP Dependency-Track?
> É uma plataforma de gestão de dependências integrada ao NIST National Vulnerability Database, ao VulnDB e a outras fontes públicas. Classifica as dependências por nível de risco. → [[OWASP Dependency-Track]]

> [!question]- Como tirar mais proveito do Dependency-Track?
> Integrar à pipeline de CI, monitorar regularmente os portfólios, criar uma política de aceitação de dependências e treinar a equipe.

> [!question]- WebGoat × Juice Shop?
> WebGoat: lições isoladas, uma vulnerabilidade por vez, disponível em várias tecnologias. Juice Shop: e-commerce deliberadamente inseguro, com desafios contínuos e mais realistas, só em JavaScript/Node.js. → [[OWASP Juice Shop e WebGoat]]

> [!question]- O que significa "Goat" em WebGoat?
> Bode, em inglês: simboliza ser um alvo para práticas de segurança.

> [!question]- Cite seções do OWASP Web Security Testing Guide.
> Information Gathering, Configuration and Deployment Management Testing, Identity Management Testing, Authentication Testing, Session Management Testing, Input Validation Testing e Error Handling Testing. → [[OWASP Web Security Testing Guide]]

> [!question]- Qual seção do WSTG cobre SQL Injection e XSS?
> Input Validation Testing.

> [!question]- Qual ferramenta OWASP foi usada no Hands On para achar vulnerabilidades?
> O OWASP ZAP.

## Aula 6 - Padrões de segurança
> [!question]- Quantos pilares tem o Well-Architected, e qual é o destaque da disciplina?
> 6 pilares. O destaque é o de segurança. → [[AWS Well-Architected]]

> [!question]- Quais ferramentas da AWS avaliam a nuvem?
> AWS Well-Architected Tool, Trusted Advisor e AWS Security Hub.

> [!question]- Quais são os 4 padrões verificados pelo AWS Security Hub?
> Melhores práticas de segurança básicas da AWS, CIS AWS Foundations Benchmark, PCI DSS e NIST 800-53.

> [!question]- Quem criou o CIS AWS Foundations Benchmark, qual é a versão e quantos níveis de conformidade ela tem?
> O Center for Internet Security (CIS). Versão 1.4.0, com 2 níveis de conformidade. → [[CIS AWS Foundations Benchmark]]

> [!question]- Como o PCI DSS protege os dados dos titulares de cartão?
> Criptografando os dados sensíveis e mascarando (truncando) o número do cartão, exibindo só partes dele. → [[PCI DSS]]

> [!question]- Quais são as funções essenciais do NIST, segundo a aula 6?
> Identificar, Proteger, Detectar, Responder e Recuperar.

> [!question]- Quais são os principais pontos da ISO 27001 na aula 6?
> Escopo e contexto, Política de Segurança da Informação (PSI), e avaliação e tratamento de riscos (mitigar ou aceitar).

> [!question]- Quais são os 4 controles principais da ISO 27002 na aula 6?
> Políticas de segurança da informação, gestão de ativos, segurança em recursos humanos e controle de acesso.

## Dúvidas em aberto
- [ ] **Aula 1**: o resumo cita "a diferença entre ataque, vulnerabilidade e intrusões", mas o texto do PDF não define esses termos. Conferir no vídeo.
- [ ] **Aula 2**: o título cita **buffer overflow**, e o resumo cita o impacto do XSS na **autenticação JWT**, mas o texto não detalha nenhum dos dois. Conferir no vídeo.
- [ ] **Aula 5**: a **lista do OWASP Top 10** não está no texto do PDF. Os vídeos tratam das mudanças entre 2017 e 2021 e das 4 vulnerabilidades mais comuns. Conferir no vídeo.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
