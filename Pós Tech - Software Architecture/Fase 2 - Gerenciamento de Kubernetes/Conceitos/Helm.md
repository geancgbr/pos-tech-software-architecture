---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [Helm Chart, Helm Charts, Chart, charts, Chart.yaml, values.yaml]
---

# Helm

**Ferramenta de gerenciamento de pacotes para o Kubernetes**. Empacota todos os recursos necessários para implantar um aplicativo num **chart**, guardado num **repositório** "semelhante a uma loja de aplicativos".

- **Recursos**: gerenciamento de pacotes · **de versões** (reimplantar versões anteriores) · configuração flexível (Pods, serviços, volumes, ingressos) · **repositório público** de charts · personalização · escalabilidade.
- **Chart**: pacote de recursos **pré-configurados** (Pods, serviços, ingressos...), com **nome e versão**. Pode ser personalizado, compartilhado e reutilizado.
  - **`Chart.yaml`**: nome, versão e descrição.
  - **`values.yaml`**: os valores padrão das configurações.

**Comandos**
| Comando | Para quê |
|---|---|
| `helm version` | Validar a instalação |
| `helm repo add stable https://charts.helm.sh/stable` | Adicionar o repositório stable |
| `helm repo update` | Atualizar os repositórios |
| `helm create primeiro-chart` | Criar a estrutura de um chart |
| `helm package` | Gerar o `.tgz` instalável no cluster |

Aparece em: [[K8S2 03 - Helm]]
