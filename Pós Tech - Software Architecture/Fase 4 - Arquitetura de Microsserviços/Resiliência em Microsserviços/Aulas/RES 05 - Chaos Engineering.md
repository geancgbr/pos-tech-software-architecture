---
tags: [pos-tech/fase-4, resiliencia, microsservicos, chaos-engineering, aula]
disciplina: Resiliência em Microsserviços
aula: 5
fonte: "Resiliência em microservices/Aula 05 - Chaos Engineering.pdf"
---

# RES 05 - Chaos Engineering

← [[RES 04 - Service Mesh e controle de tráfego]] · [[Resiliência em Microsserviços]]

> [!summary] Em uma frase
> **Chaos Engineering** é "quebrar coisas de propósito" de forma **controlada** para tornar os sistemas resilientes: nasceu na **Netflix** (migração para a **AWS**, **Chaos Monkey** em 2010), segue **princípios** (estado estável, hipóteses, variáveis do mundo real, produção) e uma **metodologia científica**, usa ferramentas como **Chaos Toolkit, Gremlin, Litmus e Chaos Mesh**, depende de **observabilidade** e exige **cultura**. Ver [[Chaos Engineering]].

## Hands On (vídeos)
Nas videoaulas: o primeiro experimento com o **Chaos Toolkit** (open-source, declarativo); um microsserviço básico em **Python** com monitoramento em **Prometheus e Grafana**; simulação de **falhas de rede, sobrecarga de CPU e indisponibilidade de dependências**, observando o comportamento e a recuperação.

## Origem
- Pergunta de abertura: como a **Netflix** mantém o serviço para **mais de 200 milhões** de usuários diante de falhas de servidores, rede ou até de **data centers inteiros**?
- **2008**: a Netflix migra dos data centers físicos para a **AWS**; a nuvem trouxe **incerteza** (instâncias terminadas sem aviso, zonas indisponíveis, latência variável).
- **Chaos Monkey** (Figura 1): criado por **Greg Orzell** em **2010**; encerrava **aleatoriamente instâncias EC2 em produção** durante o **horário comercial**. Lógica: se o sistema não aguenta a falha de **uma instância**, não é confiável.
- **Simian Army** (Exército dos Símios): **Latency Monkey** (atrasos artificiais entre serviços), **Conformity Monkey** (boas práticas de configuração) e **Security Monkey** (vulnerabilidades).
- Não é "quebrar aleatoriamente": é uma **disciplina científica rigorosa**, com princípios formalizados pela comunidade (Figura 2).

## Princípios
| Princípio | O que diz | Exemplo do PDF |
|---|---|---|
| **1. Definir o estado estável** (steady state) | Métricas objetivas do comportamento **normal** antes de qualquer falha (tempo de resposta, taxa de erro, throughput, disponibilidade...): a **linha de base** | E-commerce: "**95%** das buscas em menos de **500 ms**, com erro inferior a **0,1%**" |
| **2. Formular hipóteses** | Como o sistema deve se comportar sob falhas, com base na arquitetura | "Com **20%** dos servidores indisponíveis, o sistema continua normal pelo balanceamento automático, com resposta abaixo de **1 s**" |
| **3. Introduzir variáveis do mundo real** | Simular falhas que **realmente acontecem**, não cenários irreais | Hardware · rede (latência, perda de pacotes, particionamento) · recursos (CPU, memória, disco) · dependências externas · configuração (deploys com bugs) |
| **4. Executar em produção** | O mais **controverso**: ambientes de teste nunca replicam totalmente a produção. A progressão é **gradual**: desenvolvimento → staging → produção, com experimentos de **baixo risco** e salvaguardas | — |

## Metodologia de um experimento
| Etapa | O que envolve |
|---|---|
| **Observação e pergunta** | Ex.: "O que acontece se o banco principal ficar indisponível por **30 s**?"; "E se a latência subir para **2 s**?" |
| **Hipótese** | Critérios: **específica, mensurável, alcançável, relevante e temporal**. Ex.: banco principal fora por 30 s → **failover** para o secundário em menos de **10 s**, disponibilidade acima de **99%** |
| **Design** | Como introduzir a falha, métricas, duração e **critérios de parada**; efeitos colaterais e **planos de contingência** |
| **Execução controlada** | Verificar as condições iniciais, introduzir a falha **gradualmente**, monitorar, estar pronto para **interromper** e documentar |
| **Análise** | Comparar com a hipótese, achar comportamentos inesperados, registrar lições, **confirmar ou refutar** |
| **Ação e melhoria** | O objetivo é **identificar melhorias**; problemas revelados devem ser priorizados e corrigidos |

- Antes do ciclo contínuo: base de **observabilidade** e **mitigação** (monitoramento, alertas, **rollback** seguro); começar com experimentos simples e ampliar.
- **Continuous Chaos Engineering Experiment Lifecycle** (AWS Prescriptive Guide, Figura 3): experimentos como parte **regular** do desenvolvimento e das operações, com métricas, automação e feedback rápido.

## Tipos de experimentos
| Tipo | Exemplos |
|---|---|
| **Infraestrutura** | Terminação de instâncias · indisponibilidade de zonas · falhas de rede · esgotamento de recursos |
| **Aplicação** | Exceções não tratadas · vazamentos de memória · deadlocks · corrupção de dados |
| **Dependências** | APIs externas indisponíveis · bancos inacessíveis (cache e fallback) · serviços internos com falha · degradação de dependências (timeouts e circuit breakers) |
| **Segurança** | Negação de serviço (DDoS) · acesso não autorizado · injeção de dados maliciosos · vazamento de dados sensíveis |

## Ferramentas
| Ferramenta | O que o PDF diz |
|---|---|
| **Chaos Toolkit** | Open-source; experimentos **declarativos** em **JSON ou YAML**; arquitetura de **plugins**, com drivers para Kubernetes, AWS, Azure, Google Cloud, Prometheus etc. |
| **Gremlin** | Plataforma **comercial** com interface gráfica; ataques pré-configurados (CPU, memória, disco, rede, processos), agendamento, relatórios e integração com monitoramento; ideal para quem está começando |
| **Litmus** | Open-source, para **Kubernetes**; experimentos como **CRDs**, o que facilita **GitOps** |
| **Chaos Mesh** | Open-source, para **Kubernetes**; **interface web** rica e muitos tipos de falha, inclusive **corrupção de dados no sistema de arquivos** |

## Observabilidade no Chaos Engineering
- Sem observar e medir, é **impossível** saber se o experimento deu certo. Ver [[Disponibilidade e Observabilidade]].
- **Monitoramento**: coletar e alertar sobre métricas **conhecidas e predefinidas**. **Observabilidade**: entender o **estado interno** pelas **saídas externas**. No Chaos Engineering, são necessários **os dois**.
- **Três pilares** (Figura 8): **métricas** (visão quantitativa agregada; tendências, baselines, alertas) · **logs** (eventos discretos; sequência que levou ao problema) · **traces** (caminho de uma requisição; onde as falhas se propagam). Ver [[Três Pilares da Observabilidade (Logs, Métricas e Traces)]].
- Aspectos: **instrumentação** (aplicação e infraestrutura) · **correlação** (**geralmente** por identificadores como **trace IDs**) · **visualização** (dashboards) · **alertas inteligentes** (inclusive degradações sutis).

> [!note] As figuras da aula vão de 1 a 3 e depois saltam para a **Figura 8**.

## Implantação na organização
- Vai além das ferramentas: **cultura** que vê falhas como **aprendizado**, não culpa individual, com **liderança forte**.
- **Métricas de sucesso**: **MTBF**, **MTTR** (Mean Time To **Recovery**), **SLOs** e **Error Budget**; espera-se, por exemplo, **redução do MTTR** ao longo do tempo. Ver [[MTTF, MTTR e MTBF]], [[SLI, SLO e SLA]] e [[Error Budget]].
- **Governança**: critérios e processos de aprovação, documentação obrigatória, procedimentos de **emergência** para interromper e **post-mortem**.
- Começar **pequeno** (desenvolvimento ou staging) e escalar gradualmente.
- **Desafios**: **resistência cultural** a falhas propositais; equilíbrio entre risco e valor (experimentos **conservadores** demais não revelam problemas; **agressivos** demais causam impacto).
- **Tendência**: sistemas de Chaos Engineering **autônomos**, com **Machine Learning**, que **podem** identificar pontos de falha, projetar, executar e analisar experimentos sem intervenção humana.

> [!note] Na aula 1, MTTR é "Mean Time to **Repair**"; nesta aula, "Mean Time To **Recovery**".

> [!note] O "O que você viu" cita a conexão com **sistemas complexos, teoria dos jogos e resposta humana a crises**, temas que não aparecem no corpo do texto.

## Referências
Chaos Mesh · Chaos Toolkit · Gremlin · Litmus Chaos · Netflix Chaos Monkey (GitHub) · Principles of Chaos Engineering · Rosenthal e Jones, *Chaos engineering: system resiliency in practice*
