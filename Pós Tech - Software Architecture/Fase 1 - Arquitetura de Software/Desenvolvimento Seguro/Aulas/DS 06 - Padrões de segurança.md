---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 6
fonte: "Aula 6.pdf"
---

# DS 06 - Padrões de segurança

← [[DS 05 - OWASP e OWASP Top 10]] · [[Desenvolvimento Seguro]]

> [!summary] Em uma frase
> Segurança na arquitetura da nuvem com o framework [[AWS Well-Architected]] e as ferramentas da AWS. O AWS Security Hub verifica 4 padrões: melhores práticas básicas da AWS, [[CIS AWS Foundations Benchmark]], [[PCI DSS]] e [[NIST 800-53]]. A aula também trata da [[ISO 27001 e ISO 27002]].

## Hands On (vídeos)
- O framework **Well-Architected**, um padrão "quase que compartilhado entre todas as nuvens", com **6 pilares**. A apostila os nomeia assim: Performance Operacional, Otimização de Custos, Resiliência, Sustentabilidade, Eficiência de Performance e **Segurança**, que é o destaque da disciplina.
- Três ferramentas da AWS que avaliam a nuvem e dão dicas de melhoria: **AWS Well-Architected Tool**, **Trusted Advisor** e **AWS Security Hub**.

## Os padrões do AWS Security Hub
1. Melhores práticas de segurança básicas da AWS
2. CIS AWS Foundations Benchmark
3. PCI DSS
4. NIST 800-53

A **ISO 27001 e 27002** entram na aula por serem interessantes de aplicar, embora, segundo a apostila, **não sejam exatamente padrões de segurança nem padrões da AWS**.

## CIS AWS Foundations Benchmark
Framework do **Center for Internet Security (CIS)** com configurações seguras e boas práticas para a nuvem AWS. A versão **1.4.0** é a mais recente e tem **2 níveis de conformidade**. É **atualizado regularmente**.

| # | Ponto | O que cobre |
|---|---|---|
| 1 | Identidade e acesso gerenciado | Autenticação, autorização, identidades, grupos, políticas de acesso |
| 2 | Monitoramento e registro | Logs e monitoramento para detectar e responder a eventos |
| 3 | Armazenamento seguro | Serviços como o **Amazon S3**: controle de acesso e criptografia |
| 4 | Rede segura | Regras de firewall NAT, regras de segurança de grupo, **VPC** (Virtual Private Cloud), gestão de tráfego de rede |
| 5 | Segurança de máquinas virtuais (**EC2**) | Inicialização segura, gerenciamento de imagens |
| 6 | Gerenciamento de configuração | Uso do **AWS Config** para avaliar conformidade |
| 7 | Segurança da informação | Classificação e proteção adequada dos dados |
| 8 | Conformidade e integridade | Verificações regulares de conformidade e auditorias |
| 9 | Segurança em nível de aplicação | Configurações seguras do **AWS Lambda** e de bancos de dados |
| 10 | Planejamento e gestão de emergências | Planos de resposta a incidentes e continuidade de negócios |

## PCI DSS
**Padrão de Segurança de Dados para a Indústria de Cartões de Pagamento.** Surgiu quando as principais bandeiras se uniram para proteger as informações sensíveis dos titulares de cartão, diante da demanda crescente por meios eletrônicos (cartão, PIX).

| Ponto | Ações |
|---|---|
| Construir e manter uma rede segura | Firewalls; **não usar senhas padrão** |
| Proteger os dados dos titulares | **Criptografar** dados sensíveis; **mascarar (truncar)**, exibindo só partes do número do cartão |
| Política de segurança de informações | Políticas para funcionários e contratados |
| Controle de acesso | **Acesso mínimo necessário**; identificação única por pessoa |
| Monitorar e testar as redes | Monitorar acessos e rastrear eventos; testar sistemas e processos |
| Política de segurança de sistemas | Proteção contra malware; antivírus atualizado |
| Controles no desenvolvimento de aplicações | Proteger contra vulnerabilidades comuns; desenvolver sistemas seguros |
| Número de identificação único por pessoa | Identificações únicas; acesso mínimo necessário |

> [!note] Na apostila, "identificação única" e "acesso mínimo necessário" aparecem em dois pontos diferentes da lista.

A conformidade com o PCI DSS é uma **obrigação regulatória** e também uma demonstração de compromisso com a segurança, que constrói reputação de confiança.

## NIST 800-53
- O **NIST** (Instituto Nacional de Padrões e Tecnologia) promove inovação com ciência, padrões e tecnologia de medição.
- Em **fevereiro de 2013**, começou a trabalhar com o setor privado dos EUA para incorporar boas práticas numa estrutura de segurança cibernética. É amplamente adotado nos EUA.
- Tem categorias e subcategorias com planos de ação. As **funções essenciais**:

| Função | Foco | Categorias citadas |
|---|---|---|
| **Identificar** | Entender os ativos e recursos críticos | Gerenciamento de ativos, ambiente de negócios, governança, avaliação de riscos, estratégia de gerenciamento de riscos, cadeia de suprimentos |
| **Proteger** | Salvaguardas técnicas e físicas para a infraestrutura crítica | Identidade e controle de acesso, conscientização e treinamento, segurança de dados, processos de proteção, manutenção, tecnologia de proteção |
| **Detectar** | Alertar sobre ataques | Anomalias e eventos, monitoramento contínuo, processos de detecção |
| **Responder** | Responder adequadamente aos eventos | Planejamento de resposta, comunicações, análise, mitigação, melhorias |
| **Recuperar** | Resiliência e continuidade depois do ataque | Melhorias no planejamento de recuperação, comunicações |

- A **Revisão 5** é um avanço que acompanha a evolução das ameaças. Os desafios são a adaptação em ambientes dinâmicos, as atualizações contínuas, a complexidade da tecnologia e o equilíbrio entre segurança e eficiência operacional.
- A conformidade na AWS pode ser verificada no **AWS Security Hub**.

## ISO 27001 e ISO 27002
Normas globais sobre **SGSI**. A **27001** define os **requisitos** para implementar e **certificar** um SGSI. A **27002** dá **orientações e melhores práticas** para os controles.

**ISO 27001: principais pontos**
1. **Escopo e contexto**: limites e áreas do SGSI; análise do contexto (partes interessadas, requisitos legais e regulamentares).
2. **Política de Segurança da Informação (PSI)**: documentada e alinhada aos objetivos de negócio.
3. **Avaliação e tratamento de riscos**: identificar ameaças, vulnerabilidades e impactos; controles para **mitigar ou aceitar** os riscos.

**ISO 27002: principais controles**
1. **Políticas de segurança**: segurança física, acesso lógico, classificação da informação.
2. **Gestão de ativos**: identificar, classificar e proteger dados, hardware e software.
3. **Segurança em recursos humanos**: seleção, contratação e conscientização.
4. **Controle de acesso**: privilégios, autenticação, autorização.

**Benefícios**: gestão de riscos eficaz · conformidade legal e regulatória · aumento da conscientização (menos erro humano) · confiança dos stakeholders · melhoria contínua (auditorias, revisões).

> [!tip] Resumo da aula
> Sempre que possível, avalie os pontos que não estão aptos nessas ferramentas, ou que deixaram de estar por alguma mudança na rede.

## Referências
AWS: Security Hub, Well-Architected Tool, Well-Architected · Borges, *O que é ISO 27001?* (2023) · Dahn, *Um guia para a conformidade com PCI* (Stripe) · Docs AWS, *NIST 800-53 (Rev. 5)* · IBM, *O que é o NIST Cybersecurity Framework?*
