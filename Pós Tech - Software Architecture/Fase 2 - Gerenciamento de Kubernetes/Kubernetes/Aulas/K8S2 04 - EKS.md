---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 4
fonte: "Kubernetes parte 2/Aula 4.pdf (Thiago Adriano)"
---

# K8S2 04 - EKS

← [[K8S2 03 - Helm]] · [[Kubernetes]] · Próxima → [[K8S2 05 - AWS EKS na prática, parte 1]]

> [!summary] Em uma frase
> Rodar o Kubernetes no próprio ambiente exige **provisionar servidores** e assumir **toda a instalação e a gestão**. Na nuvem, não há provisionamento de hardware nem custo de gestão. O **[[EKS (Elastic Kubernetes Service)|Amazon EKS]]** é o serviço gerenciado da AWS para Kubernetes: a AWS cuida da infraestrutura e você cuida dos aplicativos.

## Hands On
Criar um cluster Kubernetes na AWS usando o conceito de **Infrastructure as Code (IaC)** e a biblioteca **AWS Cloud Development Kit (CDK)** para provisionar e gerenciar recursos de maneira automatizada e escalável. Segundo o resumo da aula, o cluster foi criado **pela console da AWS e pelo CDK**.

## Por que a nuvem
- **No próprio ambiente**: é preciso **provisionar servidores** (o PDF lembra que alguns exercícios práticos sobrecarregam um desktop ou notebook pessoal), e a **instalação e a gestão** do K8s ficam por nossa conta.
- **Que gestão, se ele faz tudo automaticamente?** O PDF diz que, "por mais que a escalabilidade promovida pela solução seja vertical", pode ser preciso um **upgrade de hardware**. E, como qualquer software, o K8s tem **atualizações, correções de bugs e melhorias de segurança**.
- **Na nuvem** (SaaS, PaaS ou IaaS), benefícios evidentes e de curto prazo:
  - **sem provisionamento** de hardware;
  - **sem custo de gestão** de hardware e software.
- **Microsoft Azure, Google Cloud (GCP), AWS e IBM Cloud** têm produtos de gestão de contêineres (ou o próprio Kubernetes) no modelo **software as a service**.

## Amazon EKS
- **Serviço gerenciado da AWS** para executar aplicativos em contêineres com o Kubernetes, **sem gerenciar a infraestrutura subjacente**.
- Usa o Kubernetes como plataforma de orquestração, então **todas as ferramentas e APIs padrão do Kubernetes** funcionam. **Tudo o que foi aprendido no ambiente local pode ser usado no EKS.**
- **Divisão de responsabilidades**: a **AWS** gerencia a infraestrutura (**servidores, rede e armazenamento**); **você** gerencia os aplicativos em contêineres.
- **Altamente escalável**, com clusters de qualquer tamanho, e **altamente disponível**: os aplicativos continuam rodando mesmo com falhas de hardware ou software.

## Criando um cluster pela console
1. Ter uma conta na AWS e fazer login no **Console de Gerenciamento da AWS**.
2. Abrir o **console do Amazon EKS**.
3. Clicar em **"Criar cluster"** e escolher a implementação:
   - **Rápida**: usa as configurações padrão.
   - **Personalizada**: permite configurar as **opções de rede** e o **control plane**.
4. **"Configurações do cluster"**: nome e **região** da AWS.
5. **"Configurações do VPC"**: a **VPC** do cluster.
6. **"Configurações do Kubernetes"**: a **versão** do Kubernetes.
7. Clicar em **"Criar"** e esperar o cluster ficar pronto (o tempo varia com a região e o tamanho).
8. Conectar com o **kubectl**, que precisa ser **instalado e configurado** para o cluster EKS (instruções na documentação da AWS).

> [!note] No PDF, os passos 3 e 4 aparecem juntos ("3. 4. Clique no botão Criar cluster") e a numeração vai até 11. A lista acima agrupa os mesmos passos.

## Configuração do cluster
**Opções de rede**
| Opção | Características |
|---|---|
| **Amazon VPC CNI** (Container Network Interface) | **Padrão e recomendada** para a maioria dos casos: os Pods usam **IPs privados da VPC** |
| **Calico** | Solução **de terceiros** com recursos adicionais de **segurança**, como separar o tráfego entre Pods de **namespaces diferentes** |

**Control plane**: o **componente central** do Kubernetes, que **gerencia o estado do cluster** e **coordena os worker nodes**. A configuração inclui a **versão do Kubernetes**, as **opções de segurança** e a **autenticação e autorização**, pelo **Console** ou pelo **AWS CLI**.

**Worker node**: os **servidores que executam os Pods**. A configuração inclui o **tipo, o tamanho e o número de instâncias**, além das opções de **segurança** e de **armazenamento**.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
