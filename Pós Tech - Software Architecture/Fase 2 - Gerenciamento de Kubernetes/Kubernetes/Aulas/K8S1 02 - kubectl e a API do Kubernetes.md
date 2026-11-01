---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 2
fonte: "Kubernetes/Aula 2.pdf (Thiago Adriano)"
---

# K8S1 02 - kubectl e a API do Kubernetes

← [[K8S1 01 - Introdução ao Kubernetes]] · [[Kubernetes]] · Próxima → [[K8S1 03 - Pods, rótulos e anotações]]

> [!summary] Em uma frase
> O **[[kubectl]]** é o CLI para interagir com um cluster Kubernetes: implantar, atualizar, gerenciar, ver o status e depurar. Ele fala com a **API do Kubernetes** (RESTful), usando o **kubeconfig** para saber como se conectar.

## Hands On (vídeos)
Os comandos básicos do kubectl em exemplos práticos e o acesso à **API RESTful do Kubernetes com C#**.

## kubectl
- **CLI** para interagir com um cluster. É a **ferramenta principal** de administradores, devs e outros usuários para gerenciar, implantar e monitorar aplicativos.
- O **Kubernetes** é uma plataforma **de código aberto para orquestração de contêineres**, para implantar, dimensionar e gerenciar aplicativos em qualquer ambiente (local, nuvem pública ou privada).
- Gerencia **objetos Kubernetes**: pods, serviços, implantações, ingressos e outros.
- **Como funciona**: roda na máquina local e se conecta ao cluster pela **API do Kubernetes**, com **solicitações RESTful** para criar, atualizar ou excluir objetos.
- **kubeconfig**: o arquivo de configuração com o **endereço do servidor da API**, as **credenciais** e o **contexto do cluster** atual.

**Recursos**
- **Implantação**: criar pods e objetos relacionados (serviços, ingressos, volumes persistentes).
- **Atualização**: alterar a imagem do contêiner ou outras configurações.
- **Gerenciamento de objetos**: criar, excluir e modificar.
- **Status**: pods em execução, serviços em uso.
- **Solução de problemas**: logs dos contêineres, conectar-se a um contêiner em execução.

Rodar **`kubectl`** sem parâmetros mostra todas as opções, divididas em comandos **básicos, intermediários, de implantação e de gerenciamento** (Figura 1).

## Comandos principais: get, create e delete
- **`get`**: informações sobre a saúde e as configurações do cluster. **`create`**: criação. **`delete`**: remoção de recursos.

```bash
kubectl run nginx --image=nginx:1.14.2 --port:80   # assim está no PDF
kubectl get pods
kubectl delete pod nginx
```
- `kubectl run nginx ...` cria um pod chamado **"nginx"** (o nome pode ser qualquer um) a partir da imagem **nginx:1.14.2** do repositório central.
- `kubectl get pods` confere se o pod foi criado e qual é o status.
- `kubectl delete pod nginx` remove o pod.

> [!warning] Cuidado ao excluir pods
> Remover um pod pode afetar a disponibilidade de um serviço ou aplicação. Verifique se a ação não afeta outras partes do sistema.

## A API do Kubernetes
- É a **principal interface** com o cluster: ferramentas e aplicativos a usam para gerenciar pods, serviços, deployments e outros objetos.
- É **extensível e flexível** e **RESTful**, acessível com **GET, POST, PUT e DELETE**.
- É dividida em **grupos**. O grupo **"core"** tem os recursos fundamentais (pods, serviços, replicaset), e outros grupos tratam de monitoramento, segurança e armazenamento.
- **Acesso**: pelo kubectl ou por clientes próprios em **Python, Go, Java, Ruby** e outras linguagens. Há também uma **API de serviço** para aplicativos **dentro do cluster** acessarem a API.

## Referência
Bass, Clements e Kazman, *Software Architecture in Practice* (2012)
