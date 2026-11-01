---
tags: [pos-tech/fase-5, lgpd, nuvem, aula]
disciplina: Privacidade de Dados e LGPD
aula: 5
fonte: "Aula 05- LGPD na implementação da solução de tecnologia.pdf"
---

# LGPD 05 - LGPD na implementação da solução de tecnologia

← [[LGPD 04 - Inteligência artificial na LGPD]] · [[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 06 - LGPD no desenvolvimento de software]]

> [!summary] Em uma frase
> Soluções atuais integram componentes de terceiros (**IaaS, PaaS, SaaS**), mas não controlamos todo o funcionamento deles. No **IaaS**, a maior parte da segurança é da equipe que implanta; no **PaaS/SaaS**, **em muitos casos** os dados ficam com o terceiro, mas **quem usa o serviço continua responsável**. Os fornecedores de nuvem documentam sua adequação à LGPD, e o **NIST Cybersecurity Framework** organiza a segurança em cinco funções: **Identificar, Proteger, Detectar, Responder e Recuperar**.

## Hands On
Com exemplos, as implicações de segurança em soluções que coordenam vários componentes: a coordenação, a comunicação de dados entre eles e as **obrigações e limites de responsabilidade** de cada serviço.

## Serviços em nuvem
"Serviços em nuvem" e "serviços gerenciados" **na maioria das vezes** expressam a mesma coisa. Ver [[IaaS, PaaS e SaaS]].

| Tipo | O que o PDF diz |
|---|---|
| **IaaS** (Infraestrutura como Serviço) | Recursos de infraestrutura de TI online (servidores, software, datacenter, rede) comprados **sob demanda**, pagando pelo uso |
| **PaaS** (Plataforma como Serviço) | Ambiente para construir aplicações sem se preocupar com a infraestrutura; já foi conhecido como **hosting de aplicações**; automatiza desenvolvimento, teste, implementação, manutenção e hospedagem |
| **SaaS** (Software como Serviço) | Aplicativos na nuvem usados pelo navegador ou app, sem instalar; o fornecedor gerencia infraestrutura, plataforma e software. Como componente de uma solução, atua **sempre** como ferramenta **altamente especializada** para uma funcionalidade |

## IaaS
- O foco é a segurança dos **servidores e serviços**, como num ambiente próprio, com granularidade maior: sistema operacional, servidores especializados (ex.: bancos de dados) e aplicações. Inclui instalação, monitoramento, manutenção, **patches**, incidentes e desempenho, rede, privilégios de acesso e comunicação interna e externa.
- A preocupação é **compartilhada**: o fornecedor **pode** sugerir boas práticas e fornecer ferramentas, mas a **maior parte da responsabilidade** é da equipe técnica que implementa.
- **Primeiro ponto (LGPD)**: cuidado extremo com o armazenamento e manejo dos dados; o fornecedor responde só pela qualidade de funcionamento do recurso. **Exemplo**: invasão de um servidor de banco de dados por falha na implementação ou manutenção não é responsabilidade do fornecedor do "servidor virtual", nem de responder judicialmente.
- **Segundo ponto**: desenhar a comunicação de rede de forma **segregada** (ex.: redes privadas e sub-redes). Orientação comum: serviços em **sub-redes privadas**, com acesso via **roteamento** entre servidores.

## PaaS e SaaS
- Em muitos casos, os dados ficam num ambiente **controlado totalmente por terceiros**; muda o **nível de comprometimento** dos dados.
- **Exemplo (PaaS)**: usar um **MongoDB como serviço**; o fornecedor assume grande parte das preocupações da instalação manual. Mas os dados estão **terceirizados**: o **operador** dos dados responde diretamente por qualquer infração do terceiro; o terceiro só fornece e opera o serviço. Ver [[DBaaS (Database-as-a-Service)]].
- **Avaliar** termos de serviço, **SLAs** e políticas de segurança. Mitigar o risco em duas frentes: garantir que o provedor esteja em conformidade (inclusive a **localização dos data centers**) e criar um processo claro de **auditoria**.
- **Gestão do acesso**: continua com a empresa que coleta os dados; controle rigoroso de permissões (autorização), autenticações robustas, **sempre que possível com transparência total** sobre como as identidades são verificadas, e monitoramento. Funcionários e pessoas do provedor só com o **acesso necessário**. Ver [[Princípio do Menor Privilégio]].
- **Resposta a incidentes**: planos bem documentados, com definição e limites de responsabilidade; a natureza dinâmica do PaaS **pode** dificultar a resposta, então uma estratégia **proativa** **pode** fazer a diferença.

## Os fornecedores de nuvem e a LGPD
- **AWS, Google e Microsoft** têm documentação extensa sobre sua adequação.
- Uma das primeiras medidas foi **revisar contratos e termos de serviço**, que precisam ser claros sobre os dados coletados, o propósito e o armazenamento e processamento.
- Investimento em **criptografia avançada**, **monitoramento em tempo real** e soluções para os clientes controlarem seus dados; e em **treinamento** das equipes e dos usuários diretos dos produtos.

## NIST Cybersecurity Framework
Criado pelo **Instituto Nacional Estadunidense de Padrões e Tecnologia**; padrões, diretrizes e práticas para validar se a solução adere a um padrão de segurança validado e disseminado. Ver [[NIST Cybersecurity Framework]].

| Função | O que o PDF diz |
|---|---|
| **Identificar** | Compreensão organizacional do risco (sistemas, pessoas, ativos, dados, recursos); um **inventário** de ativos (dados, equipamentos, serviços, políticas, pessoas e sistemas), base dos próximos passos |
| **Proteger** | Proteções para os serviços críticos; não só técnicas, **muitas vezes físicas** (segregação de ambientes, redes isoladas); controle de acesso, processos de segurança, atualização e treinamento |
| **Detectar** | Identificar eventos de segurança por **anomalias** em relação ao uso esperado; em grande parte, **monitoramento contínuo automatizado** |
| **Responder** | Plano de ação com três pontos: **planejamento** da resposta, **comunicação** do problema e **análise, mitigação e melhoria** |
| **Recuperar** | Planos de **resiliência** e restauração dos recursos afetados, de acordo com as políticas de segurança |

- **Exemplo (componente de armazenamento)**: identificar = documentação, configurações, riscos e estratégia; proteger = uso, acesso permitido e auditado, premissas como **acesso mínimo** e **anonimização**; detectar eventos; responder com plano predeterminado (causa, comunicação, documentos de melhoria); recuperar com o menor impacto.
- **Não é mandatório** implementar tudo manualmente: ferramentas de monitoramento de rede, cópia automatizada, controle de identidade e acesso e monitoramento de ambiente **podem** ser adicionadas; mesmo com mais custo e complexidade, trabalhando de forma **autônoma**, são mais eficazes.

## O que você viu
A preocupação com os dados é do **operador dos dados**. Com soluções distribuídas, a responsabilidade passa a ser entender como os componentes observam a LGPD, usá-los adequadamente e criar **mecanismos de auditoria**.

## Referências
AWS: Privacidade de dados no Brasil; Segurança na Nuvem · Google Cloud: LGPD · IBM: NIST Cybersecurity Framework · Microsoft: Privacidade no Azure · U.S. Chamber of Commerce / NIST: guia de segurança cibernética para infraestrutura crítica
