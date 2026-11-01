---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 3
fonte: "Kubernetes parte 2/Aula 3.pdf (Thiago Adriano)"
---

# K8S2 03 - Helm

← [[K8S2 02 - Logs e monitoramento com EFK]] · [[Kubernetes]] · Próxima → [[K8S2 04 - EKS]]

> [!summary] Em uma frase
> O **[[Helm]]** é uma ferramenta de **gerenciamento de pacotes** para o Kubernetes. Ele empacota todos os recursos necessários para implantar um aplicativo num **chart**, guardado num **repositório** "semelhante a uma loja de aplicativos", e tem comandos para **implantar, atualizar e desinstalar**.

## Hands On
O Helm e como usá-lo para criar charts próprios. Os charts são compostos por **arquivos YAML** que descrevem os recursos do Kubernetes necessários para implantar um aplicativo ou serviço, e o Helm instala e atualiza esses pacotes.

## O Helm
- Permite a **implantação e o gerenciamento simplificados** de aplicativos em contêineres no Kubernetes, empacotando todos os recursos num pacote chamado **chart**.
- Os charts ficam num **repositório**, semelhante a uma loja de aplicativos, onde se pesquisa e se implanta no cluster.
- Tem um conjunto de **comandos de linha de comando** para implantar, atualizar e desinstalar aplicativos.

| Recurso | O que permite |
|---|---|
| **Gerenciamento de pacotes** | Empacotar tudo o que o aplicativo precisa num **chart** |
| **Gerenciamento de versões** | Gerenciar versões de um chart e **reimplantar versões anteriores** |
| **Configuração flexível** | Configurar os recursos: **Pods, serviços, volumes e ingressos** |
| **Repositórios de charts** | Um **repositório público** de charts para pesquisar e implantar |
| **Personalização do chart** | Adicionar recursos novos e modificar os existentes |
| **Escalabilidade** | Implantar em clusters de **qualquer tamanho**, do teste à produção |

## Instalação
1. Baixar o binário no **site oficial do Helm**, numa versão **compatível com a do Kubernetes** usada.
2. **Linux**: extrair e copiar para `/usr/local/bin`, para rodar `helm` de qualquer lugar:
   ```bash
   tar -zxvf helm-VERSION-linux-amd64.tar.gz
   sudo mv linux-amd64/helm /usr/local/bin/helm
   ```
   **Windows**: extrair, copiar para um diretório de bibliotecas e adicioná-lo ao **path** (Figura 1).
3. Validar com **`helm version`** (Figura 2).
4. Adicionar o repositório **stable** e atualizar (Figura 3):
   ```bash
   helm repo add stable https://charts.helm.sh/stable
   helm repo update
   ```

## Helm Charts
- **Pacotes de recursos pré-configurados** com tudo o que é preciso para implantar um aplicativo: **Pods, serviços, ingressos** e outros objetos.
- Cada chart tem **nome e versão**. Podem ser **personalizados**, **compartilhados e reutilizados** entre projetos e equipes, e há uma **comunidade ativa** que contribui com charts novos e atualizações.

**Criando e empacotando**
| Passo | Comando | Resultado |
|---|---|---|
| Criar | `helm create primeiro-chart` | Estrutura de diretórios com **`Chart.yaml`** e **`values.yaml`** (Figura 4) |
| Adicionar recursos | — | Pods, serviços, ingressos etc. no diretório do chart |
| Empacotar | `helm package` | Um arquivo **`.tgz`** que pode ser instalado no cluster |

- **`Chart.yaml`**: informações sobre o chart (**nome, versão e descrição**).
- **`values.yaml`**: os **valores padrão** das configurações do Kubernetes.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
