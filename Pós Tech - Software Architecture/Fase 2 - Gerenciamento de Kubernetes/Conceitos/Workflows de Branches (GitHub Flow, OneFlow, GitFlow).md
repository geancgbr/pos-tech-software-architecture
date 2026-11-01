---
tags: [pos-tech/fase-2, devops, conceito]
aliases: [GitHub Flow, OneFlow, GitFlow, Git Flow, Branch, Branches, Merge, Rebase, Estratégia de branches]
---

# Workflows de Branches (GitHub Flow, OneFlow, GitFlow)

**Branch**: sair da linha principal e trabalhar sem mexer nela. **Workflow**: a receita de um pipeline com branches e tags. Não há padrão único.

**Critérios de escolha**: produtividade · coerência (tamanho da equipe) · praticidade (desfazer erros) · simplicidade (carga cognitiva).

| | GitHub Flow | OneFlow | GitFlow |
|---|---|---|---|
| Origem | "Lightweight", desde 2011 | Alternativa ao GitHub Flow | Vincent Driessen, 2010; o mais difundido |
| Branches principais | master/main, sempre entregável | Uma de produção; as outras são temporárias | **master** (produção) e **develop** (em andamento) |
| Branches de apoio | Branches de recurso (ex.: `oauth-feature`) | Release (com tag) e hotfix (a partir da release anterior) | **feature**, **release**, **hotfix** |
| Integração | Pull request (também para code review), merge direto na principal, deploy imediato | Tag na release, depois merge para a principal | Merge sem Fast Forward |
| Ideal para | Uma versão única em produção; amigável para delivery/deployment contínuos | Uma versão única em produção | Não citado (é o modelo mais conhecido; a maioria das empresas adota a nomenclatura Git Flow) |
| Não indicado | Releases de homologação; várias versões em produção | Projetos com homologação; várias versões em produção | Não citado |
| Outras vantagens e desvantagens | Desvantagem: o código em produção pode ficar instável | Vantagens: histórico do git mais limpo e legível; flexível | Não citadas |

**Merge × rebase**: o resultado é basicamente o mesmo. O **rebase** deixa o histórico mais limpo. O **merge** cria uma linha de histórico no ponto da integração, o que é mais complexo de ler, mas **mais seguro**, porque não sobrescreve código. Analise caso a caso.

Detalhes e a tabela de comparação: [[DEV 02 - Melhores práticas com o GitHub#Comparação dos workflows]]
