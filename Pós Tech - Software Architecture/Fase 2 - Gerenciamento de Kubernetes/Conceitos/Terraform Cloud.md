---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [HCP Terraform, Terraform Enterprise, Workspaces do Terraform Cloud]
---

# Terraform Cloud

Plataforma **SaaS gerenciada pela HashiCorp** para rodar o Terraform **em equipe**, de forma remota, centralizada e automatizada. É a evolução da execução local.

**Recursos**: **estado remoto** (a principal característica) · também **bloqueio de estado** · colaboração, com revisão e aprovação de planos · **workspaces** por ambiente ou projeto · integração com **VCS** (GitHub, GitLab, Bitbucket) · **segredos na plataforma** · **RBAC** · automação de plan e apply.

**Quando usar**: equipes distribuídas · controle rigoroso · automação e CI/CD.

**CI/CD**: integra com Jenkins, GitLab CI, **GitHub Actions** e CircleCI. Tem logs de todas as execuções e **aprovação manual** antes de produção.

**× Terraform Enterprise**: o Enterprise tem suporte dedicado, audit logs e integração com sistemas empresariais, e pode ser hospedado **na nuvem ou on-premises**. O Cloud é SaaS e tem funcionalidades gratuitas.

Detalhes: [[TF 09 - Terraform Cloud]]
