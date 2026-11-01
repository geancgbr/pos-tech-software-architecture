---
tags: [pos-tech/fase-1, arquitetura, aula]
disciplina: Arquitetura de Software
aula: 4
fonte: "Aula 4 - Arquitetura de Software_revFinal.pdf"
---

# ARQ 04 - Escalabilidade, disponibilidade e desempenho

← [[ARQ 03 - Documentação, testabilidade e modificabilidade]] · [[Arquitetura de Software]] · Próxima → [[ARQ 05 - Arquitetura Hexagonal]]

> [!summary] Em uma frase
> Pontos que ajudam na escalabilidade e na resiliência da aplicação: [[Escalabilidade]], [[Disponibilidade e Observabilidade]] e [[Desempenho]], com destaque para monitoramento e [[Estratégias de Cache|cache]].

## Hands On (vídeos)
- **Health check**: monitora a saúde da aplicação, por exemplo se ela está conectada ao banco de dados.
- **Zabbix**: ajuda no monitoramento com disparo de notificações.
- **Prometheus e Grafana**: monitoramento e disponibilidade. Os docentes implementaram as bibliotecas no projeto e criaram containers com **Docker** para demonstrar.
- **Azure Container Apps**: serviço em cloud, um PaaS para Kubernetes, usado para escalar a aplicação.

## Escalabilidade
- **Definição**: capacidade de o sistema **crescer e se adaptar** a um aumento de demanda (usuários, dados, tráfego de rede) **sem prejudicar desempenho ou confiabilidade**.
- **Estratégias**:
  - **arquitetura escalável**: sistemas distribuídos e balanceamento de carga;
  - **tecnologias modernas**: computação em nuvem e contêineres;
  - **banco de dados escalável**: NoSQL e tecnologias de cache;
  - **monitoramento e otimização**: frequentes, para garantir escalabilidade a longo prazo.

## Ferramentas de monitoramento e otimização
| Ferramenta | O que é, segundo a apostila |
|---|---|
| **New Relic** | Monitoramento e análise de desempenho, com visibilidade em tempo real do aplicativo, da infraestrutura e dos usuários finais |
| **Nagios** | Código aberto. Monitora serviços de rede, servidores e dispositivos de rede em tempo real e envia alertas |
| **Splunk** | Análise e inteligência de dados de várias fontes, como logs de aplicativos, infraestrutura e segurança |
| **AppDynamics** | Monitoramento de desempenho de aplicativos empresariais em tempo real, identificando problemas na experiência do usuário |
| **VisualVM** | Código aberto, para aplicativos **Java**: memória, threads, classes e outros recursos |

## Disponibilidade × observabilidade
| | Disponibilidade | Observabilidade |
|---|---|---|
| O que é | Capacidade de o sistema **estar disponível** para uso quando necessário | Capacidade de **observar e medir** o comportamento do sistema **em tempo real** |
| Como se mede | **Tempo de atividade** em relação ao tempo total | **Métricas de desempenho**: tempo de resposta, taxa de erros, utilização de recursos |

São **complementares**. Um sistema muito disponível ajuda pouco se não puder ser observado para detectar problemas, e um sistema muito observável ajuda pouco se não estiver disponível. As equipes devem monitorar as duas coisas.

## Desempenho
- **Definição**: quão bem um sistema executa uma tarefa em relação às expectativas ou aos requisitos, de forma eficiente e eficaz.
- **Dimensões**: tempo de resposta, taxa de transferência, utilização de recursos, confiabilidade e escalabilidade.

## Cache
Armazena temporariamente em memória os dados acessados com frequência, para não buscá-los de novo na origem (banco de dados, sistema de arquivos). Assim reduz o tempo de busca e melhora a resposta.

| Estratégia | O que vai para o cache |
|---|---|
| **Página inteira** | A página toda (HTML, CSS, JS e outros recursos) |
| **Banco de dados** | Dados acessados com frequência, como perfil do usuário |
| **Objeto** | Objetos complexos ou recursos muito usados (imagens, JSON) |
| **Sessão** | Dados da sessão: preferências, histórico, carrinho |
| **CDN** | Mídia (imagens, vídeos) em servidores pelo mundo, servida do mais próximo do usuário |

O fluxo de cache está na Figura 1 do PDF.

## Referências
Fowler, S. J., *Microsserviços Prontos Para a Produção* (2017) · Majors, Fong-Jones e Miranda, *Observability Engineering* (2022)
