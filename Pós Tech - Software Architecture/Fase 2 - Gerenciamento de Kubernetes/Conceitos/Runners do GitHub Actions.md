---
tags: [pos-tech/fase-2, github-actions, conceito]
aliases: [Runner, Runners, Self-hosted runner, Runner auto-hospedado, Runners auto-hospedados]
---

# Runners do GitHub Actions

**Agentes que hospedam a execução dos jobs** de um workflow. Podem ser **hospedados pelo GitHub** (hardware e software fixos, minutos gratuitos limitados) ou **auto-hospedados (self-hosted)**.

**Por que usar self-hosted**: hardware ou software específicos · restrições de rede (recursos internos, políticas que proíbem a nuvem) · controle e gerenciamento · custo (servidores próprios ou capacidade de computação inutilizada) · configuração personalizada · desempenho.

**Responsabilidades**: manutenção, segurança, atualizações e custo da infraestrutura. É um trade-off entre **controle e conveniência**.

**Boas práticas**: isolar os workloads de produção e de dev/teste · manter atualizado · restringir o acesso e **não guardar segredos** · monitoramento e logs · recuperação de desastres e redundância · **reiniciar regularmente ou usar runners efêmeros** · gerenciar a capacidade.

**Limites** (sujeitos a alteração): workflow com até **35 dias** · job até **24 h** na fila · **1.000** requisições à API por hora por repositório · matriz com até **256** jobs · **500** execuções em fila a cada 10 s por repositório · **10.000** runners por grupo.

Os runners **auto-hospedados** são a ponte do GitHub Actions com o [[Ambiente On-Premises]].

Aparece em: [[GHA 02 - Fundamentos básicos]], [[GHA 03 - GitHub Actions em ambientes On-Premises]]
