---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 1
fonte: "Kubernetes/Aula 1.pdf (Thiago Adriano)"
---

# K8S1 01 - Introdução ao Kubernetes

[[Kubernetes]] · Próxima → [[K8S1 02 - kubectl e a API do Kubernetes]]

> [!summary] Em uma frase
> Dois problemas comuns em todo projeto, **gestão de múltiplos ambientes** e **escalabilidade**, têm uma peça em comum na solução: o **contêiner**. O **Kubernetes (K8S)** automatiza criar e destruir contêineres a partir de imagens e mantém a infraestrutura operacional. A aula prepara o ambiente com **kubectl, Docker e Minikube**.

## Hands On (vídeos)
Virtualização explicada com desenhos, Docker na prática (criando uma imagem a partir de um projeto do professor Thiago) e o básico de Kubernetes, com o **primeiro Pod**.

## Motivação
- **Gestão de múltiplos ambientes** (desenvolvimento, testes, produção): hardware, rede e infraestrutura para os devs construírem e testarem, o QA homologar e os usuários usarem. Além dos custos, é difícil manter os três **minimamente parecidos** em configuração, capacidade, dados e rede.
- **Escalabilidade (scaling)**: a capacidade de **crescer ou encolher** a infraestrutura conforme a demanda. Exemplo: um site de vendas dimensionado para o ano inteiro, mas com pico na **Black Friday**. O que fazer com o excedente? E quando a demanda foi mal dimensionada?
- **"Para problemas complexos, não temos soluções simples"**: a solução combina **DevOps, Cloud Computing e Docker**.

## Virtualização × contêineres
| | Virtualização (VMs) | Contêineres |
|---|---|---|
| O que cria | Uma "pequena máquina" completa (**hardware e SO**) dentro da hospedeira | Uma "pequena máquina" na **camada do SO** da hospedeira |
| O que compartilha | Só os **recursos de hardware** | O **hardware e o próprio SO** |
| Peso | — (o PDF só compara) | **Muito mais leve e barata** do que uma VM, só com o software, os arquivos e as bibliotecas necessários |

- São **semelhantes, não iguais** ("muito longe disso!").
- **Exemplo**: um ambiente com **MySQL sobre Debian** é uma imagem com todos os arquivos, binários e bibliotecas; um servidor web para **Java Spring Boot**, outra imagem, "com tudo o que precisamos e nada mais".
- **Ambientes**: criar e replicar de forma simples e rápida, evitando possíveis diferenças de configuração.
- **Escalabilidade horizontal**: criar e destruir recursos computacionais **por demanda**.
- **Escalabilidade vertical**: **expandir os recursos físicos** (on-premise ou nuvem), com o hardware existente ou novos componentes.

## Kubernetes (K8S)
- Responsável por tarefas que, manuais, seriam caras e ineficientes: **criar e destruir contêineres a partir de uma imagem** e **manter a infraestrutura operacional**. Se um contêiner falha, **cabe ao K8S criar outro**.
- A arquitetura é baseada em **clusters**. Cada nó pode ter um ou mais contêineres, o que se chama **Pod** (Figura 3 do PDF).
- O Kubernetes expõe **APIs REST no nó master**. A ferramenta mais usada para acessá-las é o **Kube Control (kubectl)**, que pode ser instalado em qualquer SO e funciona como **client do nó master**: "sem dúvida a forma mais produtiva" de trabalhar com o Kubernetes.

## Preparando o ambiente
| Passo | O que instalar | Como validar |
|---|---|---|
| 1 | **kubectl** (documentação para Windows ou Linux) | `kubectl version --output=yaml` |
| 2 | **Docker**: software de plataforma aberta que implementa contêineres, com **arquitetura cliente-servidor**, para data center, cloud ou híbrido | `docker -v` |
| 3 | **Minikube**: implementação **leve** do Kubernetes que cria uma VM local com um cluster de **um nó só**, a melhor indicação para estudos e desenvolvimento local. Precisa de um mecanismo de virtualização (o Docker). Verifique os pré-requisitos de hardware | `minikube start` (baixa uma imagem do Kubernetes do repositório oficial, o que pode demorar), depois `kubectl get pods` |

## Referência
Bass, Clements e Kazman, *Software Architecture in Practice* (2012)
