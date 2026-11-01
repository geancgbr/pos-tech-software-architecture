---
tags: [pos-tech/fase-2, github-actions, aula]
disciplina: GitHub Actions
aula: 3
fonte: "Aula 03 - GitHub Actions em Ambientes On-Premises.pdf"
---

# GHA 03 - GitHub Actions em ambientes On-Premises

← [[GHA 02 - Fundamentos básicos]] · [[GitHub Actions]] · Próxima → [[GHA 04 - Conceitos básicos de Docker]]

> [!summary] Em uma frase
> Num ambiente **[[Ambiente On-Premises|On-Premises]]** (infraestrutura dentro da organização), o GitHub Actions usa **[[Runners do GitHub Actions|runners auto-hospedados (self-hosted)]]**, que dão mais controle, mas exigem que a organização cuide da manutenção, da segurança e dos custos.

## Hands On
Instalar e configurar um servidor local (On-Premises) para o GitHub Actions, configurar o GitHub Actions nele (criação e gerenciamento de workflows), usar ações para compilação, testes e implantação, e cenários reais de uso.

## Ambientes On-Premises
**Infraestrutura de TI mantida fisicamente dentro da organização**, ao contrário da nuvem, que é hospedada remotamente e acessada pela internet. "On-premises" quer dizer **"no local"**.

| Vantagens | Desvantagens |
|---|---|
| **Controle total** de sistemas e dados (crucial com informações sensíveis) e personalização completa | **Custo**: hardware, manutenção, atualização, segurança e pessoal qualificado |
| **Segurança**: a organização define e implementa suas próprias políticas | **Escalabilidade**: aumentar a capacidade exige planejamento, compra e instalação de servidores |
| **Conformidade**: regulamentações que exigem dados armazenados localmente | **Inatividade e recuperação**: a empresa responde pela redundância e pela recuperação de desastres, o que é caro e complexo |

A escolha entre On-Premises e nuvem depende de conformidade, controle de dados, segurança, custo e escalabilidade.

## Runners
- **Runners são agentes que hospedam a execução dos jobs** de um workflow.
- O GitHub oferece **runners hospedados** na infraestrutura dele, mas em ambientes On-Premises pode ser melhor usar **runners auto-hospedados (self-hosted)**.

**Quando usar runners auto-hospedados**
| Situação | Por quê |
|---|---|
| **Hardware ou software específicos** | Os runners do GitHub têm um conjunto fixo |
| **Restrições de rede** | Acessar recursos da rede interna, ou políticas que não permitem rodar na nuvem |
| **Controle e gerenciamento** | Atualizações, patches e monitoramento conforme as suas políticas |
| **Custos** | Passar dos minutos gratuitos gera custo; se você tem seus próprios servidores ou muita capacidade de computação inutilizada, pode ser mais econômico |
| **Configuração personalizada** | Software, dependências e ferramentas da sua base de código |
| **Desempenho** | Pode ser mais rápido em máquinas locais, com cargas pesadas |

**Responsabilidades**: gerenciar e manter os runners **seguros e atualizados** e arcar com o custo da infraestrutura. É um **trade-off entre controle e conveniência**.

## Boas práticas com runners auto-hospedados
- **Isolamento de workloads**: separar produção de desenvolvimento e teste, para evitar contaminação cruzada.
- **Gerenciamento de atualizações**: o software do runner, o SO e as dependências.
- **Segurança do runner**: limitar quem envia jobs e o que o runner pode fazer; **não guardar segredos** nele.
- **Monitoramento e logging**: para resolver problemas rápido, auditoria e conformidade.
- **Recuperação de desastres e redundância**: runners de backup, ou um plano para migrar para os runners do GitHub.
- **Rotatividade regular**: reiniciar com frequência ou usar runners **efêmeros**, para reduzir ameaças persistentes.
- **Gerenciamento de capacidade**: mais runners nos picos e hardware diferente para jobs diferentes.

## Limites com runners auto-hospedados
Os limites estão sujeitos a alterações.

| Limite | Valor |
|---|---|
| Tempo de execução do workflow | **35 dias** (incluindo espera e aprovação); depois disso, é cancelado |
| Tempo na fila do job | **24 horas**; se não começar, o job falha |
| Requisições à API do GitHub | **1.000 por hora**, somando todas as ações de um repositório |
| Matriz de jobs | **256 jobs** por execução (vale também para os runners do GitHub) |
| Fila de execução | **500 execuções a cada 10 segundos** por repositório |
| Registro de runners | **10.000** por grupo de runners |

> [!note] O texto diz "como mencionado anteriormente, runners são agentes...", mas a aula 2 só cita o runner de passagem ("mesma instância de runner").

## Referências
GitHub Docs: About self-hosted runners, Adding self-hosted runners, Configuring the self-hosted runner application as a service, Security hardening, Sobre executores auto-hospedados, Usage limits
