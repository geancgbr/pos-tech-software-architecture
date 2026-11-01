---
tags: [pos-tech/fase-2, devops, aula]
disciplina: DevOps (IaC and CI/CD)
aula: 2
fonte: "Aula 2 - DevOps - Melhores práticas com o GitHub_revFinal.pdf (Fabiano da Silva Carneiro)"
---

# DEV 02 - Melhores práticas com o GitHub

← [[DEV 01 - CI-CD principais conceitos]] · [[DevOps (IaC and CI-CD)]] · Próxima → [[DEV 03 - Testes automatizados com CI]]

> [!summary] Em uma frase
> O código-fonte é a matéria-prima do software, e o versionamento deve ser tratado com alto rigor, como o cofre de um banco. O [[Controle de Versão|versionamento]] pode ser **centralizado ou distribuído** (o mais indicado para CI), e a colaboração funciona com uma boa **estratégia de branches**: **[[Workflows de Branches (GitHub Flow, OneFlow, GitFlow)|GitHub Flow, OneFlow ou GitFlow]]**.

## Hands On
Ferramentas de versionamento, estratégias de branches para diferentes fluxos de um pipeline DevOps e o **primeiro deploy com o GitHub Actions**. O PDF traz o link "Códigos da aula 2".

## Por que versionar
- Sem o código-fonte guardado, não dá para corrigir nem evoluir o software: seria preciso **recriá-lo totalmente**. É o tema que mais gera problemas e retrabalho nas empresas.
- Em ambientes profissionais, o versionamento é tratado com **alto rigor**, como o **cofre de um banco**, com processo estruturado e um passo a passo para acessá-lo. E deve ser feito da forma mais **otimizada**, sem processos manuais.
- **Controle de versão** (Chacon e Straub, 2014): registra as alterações de arquivos ao longo do tempo para recuperar versões específicas. Permite reverter arquivos ou o projeto inteiro, comparar alterações, ver quem modificou por último e quem introduziu um problema, e quando, além de recuperar arquivos perdidos, tudo com pouca sobrecarga.

## Centralizado × distribuído
| | Centralizado | Distribuído |
|---|---|---|
| Como funciona | **Um único servidor** com o código. Os devs retiram os arquivos e devolvem atualizados | Os devs **espelham o repositório inteiro, com todo o histórico**: cada um tem um backup completo |
| Vantagens | Todos sabem o que os outros estão fazendo; os administradores têm controle completo | Se o servidor falhar, o time continua e ainda pode restaurá-lo; permite configurar **vários fluxos de trabalho** |
| Desvantagens | **Ponto único de falha**: servidor fora do ar, ninguém versiona nem acessa; sem backup, perde-se tudo | Exige **mais disciplina**; pode gerar **muitos conflitos** com muitos times em paralelo |
| Ferramentas | CVS, Apache Subversion | GitHub, Bitbucket, GitLab |

**O distribuído é o mais indicado para CI**, porque vários times trabalham em paralelo (ex.: o time de qualidade guarda os testes automatizados, e o de infraestrutura, as automações de provisionamento). Mas a colaboração pode virar dor de cabeça: o problema está **em como ela é abordada**, não na colaboração em si.

## Branches e workflows
- **Branch** (ramificação): sair da linha principal e continuar trabalhando sem mexer nela. É como uma **pasta com nome padronizado**, controlada por um servidor.
- **Workflow**: uma receita para implementar um pipeline de forma consistente, com branches e tags. **Não há padrão único nem framework oficial.**
- **Critérios de escolha**:
  - **Produtividade**: o workflow melhora ou limita?
  - **Coerência**: foi dimensionado para o tamanho da equipe?
  - **Praticidade**: é fácil desfazer erros?
  - **Simplicidade**: impõe sobrecarga cognitiva desnecessária?

### GitHub Flow
- Um "**lightweight workflow**", criado a partir de **2011**.
- **Tudo na master/main pode ser entregue.** A única regra inviolável: se houver problemas em commits, eles são **revertidos** ou **novos commits** são adicionados.
- Branches de recurso saem da principal, sem nomenclatura pré-definida (ex.: `oauth-feature`). O que não está na principal é **WIP** (Working in Progress).
- **Pull requests** preparam o merge e servem para **code review**, e podem ser obrigatórios. Depois do aceite, o merge vai **direto na principal**, sem branches intermediárias. Tudo o que entra na principal vai **imediatamente** para o ambiente.
- **Vantagens**: amigável para delivery/deployment contínuos; ideal com **uma versão única** em produção.
- **Desvantagens**: o código em produção pode ficar instável; não serve para releases de homologação; não é recomendado com **várias versões** em produção.

### OneFlow
- Criado como **alternativa ao GitHub Flow**. Toda nova versão em produção é **baseada na release anterior**.
- **Uma única branch de produção** (nome não padronizado); todas as outras são **temporárias**.
- **Releases**: branches de release a partir de um commit escolhido da master/main. Quando estão prontas, cria-se uma **tag** na branch de release e faz-se o **merge** para a principal.
- **Hotfix**: uma branch a partir da release usada na entrega anterior; ao terminar, a mesma regra de tags.
- **Vantagens**: histórico do git **mais limpo e legível**; flexível conforme as decisões da equipe; ideal com uma versão única em produção.
- **Desvantagens**: não é recomendado com processo de **homologação** nem com várias versões em produção.

### GitFlow
- O modelo **mais conhecido e difundido** nas empresas, criado por **Vincent Driessen (2010)**, baseado em **duas branches principais**.
- **master**: a versão oficial em **produção**. **develop**: a versão em andamento, que recebe o trabalho de todas as equipes.
- **Branches de suporte** (é uma sugestão; cada equipe adapta):
  - **feature**: novas funcionalidades, ainda longe da entrega;
  - **release**: quando a develop atinge as features previstas, para testes e empacotamento;
  - **hotfix**: erro em produção que precisa de correção imediata.
- O diagrama completo está na Figura 8 do PDF.

## Merge × rebase
As setas entre as branches são os momentos de integração, que podem ser feitos de duas formas, com basicamente o mesmo resultado:
- **Rebase**: histórico **mais limpo**, porque move o histórico de alterações para o início do histórico da branch de origem.
- **Merge**: gera uma **linha de histórico** no ponto da integração, o que pode complicar a leitura, mas dá **mais segurança**, porque não sobrescreve código.
- O ideal é **analisar caso a caso** (o *Pro Git* traz cenários).

## Comparação dos workflows
| | OneFlow | GitHub Flow | GitFlow |
|---|---|---|---|
| Feature/topic branches | Sim | Sim | Sim |
| Release branches | Sim | Não | Sim |
| Rebasing | Opcional | Não | Não |
| Merges | Opcional | Mediante pull requests | Sim, mas sem Fast Forward |
| Hotfix branches | Sim | Não citado | Sim |

> [!note] O texto extraído da tabela (pág. 16 do PDF) sai embaralhado na linha de **rebasing**. A distribuição acima é a leitura mais provável; confira na tabela original.

## Referências
Chacon e Straub, *Pro Git* (2014) · Driessen, *A successful Git branching model* (2010) · Microsoft, *Branch de desenvolvimento e controle do código-fonte – LUIS* (2021)
