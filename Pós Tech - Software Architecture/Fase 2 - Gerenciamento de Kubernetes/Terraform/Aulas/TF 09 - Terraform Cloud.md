---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 9
fonte: "POSTECH - Aula9_rev2.pdf"
---

# TF 09 - Terraform Cloud

← [[TF 08 - Criação de infra com AWS]] · [[Terraform]]

> [!summary] Em uma frase
> O **[[Terraform Cloud]]** é a plataforma gerenciada (SaaS) da HashiCorp para rodar o Terraform **em equipe**, de forma remota e centralizada: estado remoto com bloqueio, **workspaces**, integração com VCS e CI/CD, RBAC, segredos e aprovação manual.

## Hands On
Criar e configurar uma conta no Terraform Cloud e montar uma infraestrutura básica totalmente automatizada, integrada ao **GitHub**. Segundo a introdução, o objetivo é automatizar o CI/CD, usar **secrets** e gerenciar o **tfstate** pelo Terraform Cloud.

## O que é
- Plataforma **gerenciada pela HashiCorp** para executar e colaborar em projetos Terraform de forma **centralizada e automatizada**. Ao contrário do `terraform apply` local, permite colaboração em tempo real e integração com **VCS** (GitHub, GitLab).
- Voltado para a **IaC em equipe**: colaboração, controle de acesso e automação do ciclo de vida.
- É a **evolução da execução tradicional** em máquinas locais ou servidores privados: executa o Terraform num ambiente **remoto, controlado e escalável**.

## Principais recursos
| Recurso | O que faz |
|---|---|
| **Estado remoto** (a principal característica) | Guarda o estado de forma segura e centralizada |
| **Bloqueio de estado** | Impede que dois usuários ou processos apliquem alterações ao mesmo tempo |
| **Colaboração** | Compartilhar e ver mudanças; **revisar e aprovar planos** antes de aplicar |
| **Workspaces** | Representam ambientes ou projetos (dev, teste, produção), cada um com suas configurações e variáveis |
| **Integração com VCS** | GitHub, GitLab ou Bitbucket: alterações sincronizadas e aplicadas quando um **pull request é aceito** |
| **Segurança** | Credenciais e variáveis sensíveis **na plataforma** (não em arquivos locais ou repositórios); **RBAC** (permissões por função para executar, revisar ou aprovar) |
| **Automação** | Plan e apply automáticos quando há código novo no repositório |

## Quando usar
1. **Equipes distribuídas**, em fusos diferentes.
2. **Organizações que precisam de controle rigoroso**, com estado remoto e bloqueio.
3. **Automação e CI/CD**.

## Integração com CI/CD
- Integra com **Jenkins, GitLab CI, GitHub Actions e CircleCI**. A um commit ou pull request, o pipeline de CI/CD **pode** acionar o **`terraform plan`** e o **`terraform apply`** automaticamente.
- **Fluxos automatizados**: o Terraform roda quando há atualizações, sem execução manual, com mais agilidade e menos erro humano.
- **Ambientes separados**: um workspace por ambiente (dev, teste, produção), cada pipeline aplicando no seu.
- **Visibilidade**: logs detalhados de todas as execuções, que também podem ser acompanhados na ferramenta de CI/CD (Jenkins, GitHub Actions).
- **Aprovação de mudanças**: dá para exigir **aprovação manual** antes de aplicar em produção, uma camada extra de segurança contra mudanças acidentais.

## Terraform Cloud × Terraform Enterprise
| | Terraform Cloud | Terraform Enterprise |
|---|---|---|
| Para quem | Muitas funcionalidades **gratuitas** ou planos pagos para pequenas e médias empresas | Empresas com necessidades mais rigorosas de escalabilidade, governança e segurança |
| Recursos | Os da plataforma | Mais avançados: **suporte dedicado, audit logs, integração com sistemas empresariais** |
| Hospedagem | **SaaS**, pelo navegador | **Na nuvem ou on-premises** |

## Referências
HashiCorp: Automate Terraform with GitHub, Migrate state to HCP, Terraform Cloud login
