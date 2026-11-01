---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 4
fonte: "Kubernetes/Aula 4.pdf (Thiago Adriano)"
---

# K8S1 04 - Services e ConfigMap

← [[K8S1 03 - Pods, rótulos e anotações]] · [[Kubernetes]] · Próxima → [[K8S1 05 - ReplicaSets e Deployments]]

> [!summary] Em uma frase
> Um **[[Service do Kubernetes|Service]]** expõe um conjunto de Pods com **um único ponto de entrada** e distribui o tráfego entre eles. Há três tipos: **ClusterIP** (interno, o padrão), **NodePort** e **LoadBalancer**. O **[[ConfigMap]]** separa as configurações do contêiner dos artefatos de implantação.

## Hands On (vídeo)
Os tipos de Service em exemplos práticos, junto com o ConfigMap. Segundo o texto, a videoaula criou uma tela de login e uma API para receber os dados.

## Services
- Permitem **expor serviços dentro do cluster** e gerenciar o acesso a eles (Figura 1).
- Um Service expõe **um conjunto de Pods como um serviço**, com **um único ponto de entrada**, e **distribui o tráfego** entre os Pods, com a carga balanceada.

| Tipo | Como expõe | Acesso | Útil para |
|---|---|---|---|
| **ClusterIP** (**padrão**) | Num **IP interno do cluster** | **Só dentro** do cluster | Serviços que conversam com outros serviços do cluster |
| **NodePort** | Numa **porta do nó** do cluster | **Fora** do cluster, pelo IP do nó + a porta | Serviços acessados de fora, como aplicativos web |
| **LoadBalancer** | Num **balanceador de carga externo** | **Fora** do cluster, por um **IP externo** + a porta | Acesso externo **com balanceamento de carga** |

- **Criação**: por um **manifesto YAML** com o **tipo** de Service, o **seletor** dos Pods e as portas e protocolos.

> [!note] A Figura 2 tem a legenda "Criação de um service com ClusterIP", mas o texto descreve um **Pod** ("meu-pod", contêiner "meu-container", imagem Nginx, porta 80). As legendas das Figuras 3 a 5, sobre ConfigMap, repetem o mesmo título.

**Os campos do YAML descrito**
| Campo | Significado |
|---|---|
| `apiVersion` | A versão da API (no exemplo, `v1`) |
| `kind` | O tipo de objeto (no exemplo, `Pod`) |
| `metadata` | Os metadados, como o nome |
| `spec` | As especificações, com os contêineres |
| `containers` | A lista de contêineres (no exemplo, um) |
| `name` | O nome do contêiner ("meu-container") |
| `image` | A imagem (Nginx) |
| `ports` | As portas expostas (80) |

## ConfigMap
- **Contexto**: em microsserviços, os serviços costumam ser configurados por **variáveis de ambiente** (em YAML ou JSON), mas as configurações podem ser **extensas** ou **compartilhadas** entre vários serviços.
- **O que é**: um recurso que **separa as configurações de um contêiner dos seus artefatos de implantação**, guardando-as num **local centralizado**, gerenciado separadamente.
- **Formas de injetar no contêiner**: **variáveis de ambiente**, **arquivos montados** ou **argumentos de linha de comando**.
- **Na prática**: criar o objeto ConfigMap (Figura 3), conferir os dados (Figura 4; no exemplo está vazio) e injetar por um **objeto de implantação**. No exemplo, o contêiner **my-service-container** (imagem **my-service-image**) recebe as configurações como variáveis de ambiente pela seção **`envFrom`** (Figura 5).

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
