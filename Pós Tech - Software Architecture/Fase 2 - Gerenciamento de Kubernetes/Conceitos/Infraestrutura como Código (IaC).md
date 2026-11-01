---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [IaC, Infrastructure as Code, Infraestrutura como código]
---

# Infraestrutura como Código (IaC)

Prática em que a **infraestrutura de TI é definida e gerenciada por código**, em vez de configurações manuais ou scripts ad hoc (Terraform, aula 1).

**Benefícios**: **automação** (menos tarefas manuais) · **consistência** (menos erro humano e menos diferenças entre ambientes) · **escalabilidade** (ambientes grandes) · **rastreamento** (histórico pelo controle de versão).

**Ferramentas mais conhecidas**: **Terraform**, Ansible, Chef, CloudFormation. O Terraform se destaca pela integração com muitos provedores e pela linguagem [[HCL (HashiCorp Configuration Language)|HCL]].

Na disciplina [[DevOps (IaC and CI-CD)]], o tema não é tratado nas 4 aulas: ele é desenvolvido em [[Terraform]].

Aparece em: [[TF 01 - Introdução ao Terraform]], [[TF 08 - Criação de infra com AWS]]

**Na Fase 3**: o [[AWS SAM]] usa a sintaxe YAML do **CloudFormation** para descrever os recursos ([[SLS 06 - AWS Lambda e AWS SAM]]), e a automação de alertas com Terraform aparece na [[MAV 10 - Configurando alertas]].
