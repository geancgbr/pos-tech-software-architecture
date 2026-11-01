---
tags: [pos-tech/fase-2, kubernetes, conceito]
aliases: [ConfigMaps, envFrom]
---

# ConfigMap

Recurso que **separa as configurações de um contêiner dos seus artefatos de implantação**, guardando-as num **local centralizado**, gerenciado separadamente.

- **Problema que resolve**: em microsserviços, as configurações (variáveis de ambiente em YAML ou JSON) podem ser **extensas** ou **compartilhadas** entre serviços.
- **Formas de injetar**: **variáveis de ambiente**, **arquivos montados** ou **argumentos de linha de comando**.
- **Exemplo**: o contêiner `my-service-container` (imagem `my-service-image`) recebe o ConfigMap como variáveis de ambiente pela seção **`envFrom`** (Figura 5 do PDF da aula 4).
- Na migração do IIS para o EKS, um ConfigMap organiza os arquivos de configuração ([[K8S2 05 - AWS EKS na prática, parte 1]]).

Aparece em: [[K8S1 04 - Services e ConfigMap]]
