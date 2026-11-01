---
tags: [pos-tech/fase-2, devops, conceito]
aliases: [Versionamento, Versionamento de código, Versionamento centralizado, Versionamento distribuído, Git]
---

# Controle de Versão

Um **sistema que registra as alterações de arquivos ao longo do tempo** para recuperar versões específicas: reverter arquivos ou o projeto, comparar, ver quem alterou e quando, e recuperar arquivos perdidos (Chacon e Straub, *Pro Git*, 2014).

Deve ser tratado com **alto rigor**, como o **cofre de um banco**: sem o código-fonte, só resta recriar o software.

| | Centralizado | Distribuído |
|---|---|---|
| Modelo | Um servidor único; os devs retiram e devolvem arquivos | Cada dev tem o **repositório completo, com histórico** (backup completo) |
| Prós | Todos sabem o que os outros fazem; o administrador controla tudo | O time continua se o servidor cair; vários fluxos de trabalho |
| Contras | **Ponto único de falha**; sem backup, perde-se tudo | Mais disciplina; mais conflitos com muitos times em paralelo |
| Ferramentas | CVS, Apache Subversion | GitHub, Bitbucket, GitLab |

**O distribuído é o mais indicado para CI.** A colaboração depende da estratégia de branches: [[Workflows de Branches (GitHub Flow, OneFlow, GitFlow)]].

Aparece em: [[DEV 02 - Melhores práticas com o GitHub]]
