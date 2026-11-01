---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 9
fonte: "Kubernetes parte 2/Aula 9.pdf (Thiago Adriano)"
---

# K8S2 09 - Monitoramento e logging do EKS

← [[K8S2 08 - Segurança do AWS EKS]] · [[Kubernetes]]

> [!summary] Em uma frase
> Com vários contêineres orquestrados, os **logs** são fundamentais para analisar o que ocorre na aplicação. O EKS suporta o **Amazon CloudWatch**, o **Prometheus** (monitoramento) e o **Fluentd** e o **Fluent Bit** (logging). A aula trata do **CloudWatch**, do **[[Prometheus]]** e do **[[Grafana]]**.

## Hands On
Monitorar na prática um cluster EKS com **CloudWatch, Prometheus e Grafana**.

> [!note] O PDF diz "conforme visto na aula anterior" ao falar do EFK para monitorar clusters locais, mas o EFK foi tratado na [[K8S2 02 - Logs e monitoramento com EFK|aula 2]].

## Monitoramento e logging
- São **críticos** para gerenciar e operar clusters Kubernetes.
- O EKS suporta **Amazon CloudWatch**, **Prometheus** para monitoramento e **Fluentd** e **Fluent Bit** para logging.
- Essas ferramentas permitem que devs e equipes de operações **coletem, analisem e visualizem** informações do cluster para decisões bem-informadas, garantindo **disponibilidade e desempenho**.

## Amazon CloudWatch
- Serviço de **monitoramento e observabilidade da AWS**: coleta, visualiza e analisa **métricas, logs e eventos** de vários recursos da AWS.
- **Métricas do EKS**: criar um **grupo de recursos** do CloudWatch e configurar a coleta no cluster, pela **CLI da AWS** ou pelo **console do CloudWatch**. Para análise, há **painéis personalizados** e **alertas baseados em métricas**.
- **Logs do EKS**: configurar o **agente do CloudWatch** nos Pods ou usar o **Fluentd** para coletar e enviar os logs.

| | CloudWatch Logs | CloudWatch Logs Insights |
|---|---|---|
| O que é | **Armazena e pesquisa** logs de aplicativos e infraestrutura em escala | Ferramenta de **análise de logs** com **consultas ad hoc** |
| Detalhes | Fontes: **Amazon EKS, EC2, AWS Lambda** e mais. Os logs ficam em **grupos de logs**, cada um com vários **streams** | Filtro, agregação e visualização de resultados; **consultas em tempo real** e **dashboards personalizados** |
| Acesso / uso | Console do CloudWatch, CLI da AWS ou API do CloudWatch Logs | Facilitar a análise de logs e a resolução de problemas |

- **No EKS**: o CloudWatch Logs coleta e armazena logs de **Pods, contêineres, nós** e mais; o Logs Insights faz consultas ad hoc em tempo real. Ver a **Figura 1 do PDF** (dashboard do CloudWatch).

## Prometheus
- Sistema de **monitoramento e alerta de código aberto**: **coleta, armazena e consulta métricas**. Foi desenvolvido originalmente pela equipe do **SoundCloud** e é amplamente usado em ambientes Kubernetes.
- **Modelo pull**: os servidores de monitoramento **solicitam as métricas** dos servidores e aplicativos monitorados, em **intervalos regulares**, e as guardam num **banco de dados de séries temporais**.
- Oferece uma **linguagem de consulta flexível**, gráficos e alertas, e integra com o **Grafana** para visualização em tempo real.
- **No EKS**: coleta métricas de **Pods, contêineres e nós**. Pode ser implantado **como um conjunto de Pods** gerenciados pelo Kubernetes. Ferramentas de terceiros de integração: **kube-prometheus** e **prometheus-operator**.

## Grafana
- Plataforma de **análise e visualização de dados de código aberto**: cria e compartilha **painéis e alertas personalizados** para métricas, em tempo real.
- Suporta vários bancos de métricas, **incluindo o Prometheus**. Visualiza as métricas coletadas por ele em **painéis personalizados** de saúde e desempenho.
- **Alertas personalizados** com base em métricas específicas, para que as equipes de operações sejam notificadas **antes que os problemas se tornem críticos**.
- **EKS + Prometheus + Grafana**: coletar e visualizar métricas dos recursos Kubernetes em tempo real (**Figura 2 do PDF**).

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
