---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 5
fonte: "Aula 5.pdf"
---

# DS 05 - OWASP e OWASP Top 10

← [[DS 04 - Análise estática de código]] · [[Desenvolvimento Seguro]] · Próxima → [[DS 06 - Padrões de segurança]]

> [!summary] Em uma frase
> O [[OWASP]] é a organização que promove práticas de segurança de software e melhora a segurança de aplicações web no mundo. O principal projeto é o **OWASP Top 10**, e outros projetos são o [[OWASP Dependency-Track|Dependency-Track]], o [[OWASP Juice Shop e WebGoat|Juice Shop, o WebGoat]] e o [[OWASP Web Security Testing Guide|Web Security Testing Guide]].

## Hands On (vídeos)
- O OWASP e sua importância para a comunidade.
- O **OWASP Top 10**: as mudanças mapeadas nos estudos de **2017 e 2021** e, em detalhe, as **4 vulnerabilidades mais comuns** nos servidores do mundo.
- Prática com o **OWASP ZAP**, para encontrar vulnerabilidades no código.

> [!warning] A lista do Top 10 não está no texto do PDF
> O PDF diz que o Top 10 é o principal projeto e que ter código preparado para essas vulnerabilidades é **considerado boa prática no mercado**, mas não lista os itens. Sobre os vídeos, diz apenas que eles tratam das mudanças entre os estudos de 2017 e 2021 e detalham as 4 vulnerabilidades mais comuns.

Além dos projetos, o OWASP tem capítulos, treinamentos e Meetups.

## OWASP Dependency-Track
- **Problema**: bibliotecas evitam "reinventar a roda", mas podem ter vulnerabilidades, principalmente quando não se controla o código de todas as dependências (como visto em [[DS 03 - Bibliotecas de software|aulas anteriores]]).
- **O que é**: uma plataforma de **gestão de dependências** com uma visão abrangente de todas as dependências do projeto, para identificar e mitigar riscos de dependências inseguras.
- **Como funciona**: integra-se ao **NIST National Vulnerability Database**, ao **VulnDB** e a outras fontes públicas de vulnerabilidades conhecidas. Assim **classifica as dependências por nível de risco**, para tratar as mais críticas primeiro.
- **Como tirar mais proveito**:
  - integrar à **pipeline de CI** (avaliação automática a cada compilação);
  - **monitorar regularmente os portfólios** de dependências;
  - criar uma **política de aceitação de dependências** (o que pode e o que não pode);
  - **treinar e sensibilizar** a equipe.

## OWASP Juice Shop
Aplicação web **deliberadamente insegura**, criada pela comunidade OWASP para treinamento e sensibilização. Tem falhas das mais básicas às mais complexas, num ambiente controlado.
- **Benefícios**: aprendizado prático sem arriscar sistemas reais · sensibilização para segurança · aprimoramento de habilidades na identificação e exploração de vulnerabilidades web.

## OWASP WebGoat
Projeto **open-source** de treinamento em segurança de aplicações web. O nome junta "Web" e "Goat" (**bode**, em inglês): um alvo para praticar, explorando e corrigindo vulnerabilidades num ambiente controlado.

| | WebGoat | Juice Shop |
|---|---|---|
| **Enfoque** | **Lições**, cada uma com um desafio prático sobre uma vulnerabilidade (SQL Injection, XSS, autenticação, controle de acesso...) | **E-commerce inseguro**, com um conjunto **contínuo** de desafios numa aplicação mais complexa |
| **Ambiente** | Lições e instruções específicas, uma vulnerabilidade por vez | Experiência contínua e dinâmica: explorar, identificar e corrigir |
| **Realismo** | Mais "plataforma de treinamento", com conceitos ensinados de forma isolada | Simula um **e-commerce real** |
| **Tecnologias** | Várias: Java, .NET, Node.js... | **Só JavaScript/Node.js** |

A apostila sugere usar os dois.

## OWASP Web Security Testing Guide
Guia abrangente e prático para **testes de segurança em aplicações web**, dos conceitos fundamentais às técnicas avançadas. É **revisado periodicamente** pela comunidade.

| Seção | O que verifica |
|---|---|
| **Information Gathering** | Informações da aplicação: tecnologias, estrutura de diretórios, outros detalhes |
| **Configuration and Deployment Management Testing** | Configuração e gerenciamento de implantação |
| **Identity Management Testing** | Mecanismos de autenticação e autorização (gestão de identidade) |
| **Authentication Testing** | Força bruta, controles de senha, autenticação multifatorial |
| **Session Management Testing** | Sessões não expiradas, roubadas ou não autenticadas |
| **Input Validation Testing** | Entrada de dados: SQL Injection, XSS e outros ataques por entrada maliciosa |
| **Error Handling Testing** | Tratamento de erros e exceções, para não expor informações sensíveis |

## Referências
OWASP: Dependency-Track, Juice Shop, Top 10, Web Security Testing Guide (sites oficiais dos projetos)
