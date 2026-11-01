---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 5
fonte: "Kubernetes parte 2/Aula 5.pdf (Thiago Adriano)"
---

# K8S2 05 - AWS EKS na prática, parte 1

← [[K8S2 04 - EKS]] · [[Kubernetes]] · Próxima → [[K8S2 06 - AWS EKS na prática, parte 2]]

> [!summary] Em uma frase
> Uma proposta de **migração de um sistema publicado no IIS** (Internet Information Services) **para o EKS**, aplicando os conceitos das aulas anteriores. É a transição de uma infraestrutura **Windows e IIS** para **contêineres gerenciados pelo Kubernetes**: **avaliar** o aplicativo, **criar a imagem Docker** e **criar os objetos do Kubernetes** (Deployment, Service e Ingress).

## Hands On
- **Primeira aula**: o cenário completo que será replicado nas próximas aulas, migrando os projetos do IIS para o EKS, e a criação dos **Pods** dos projetos.
- **Aula seguinte**: criar **serviços** e um **ConfigMap** para organizar os arquivos de configuração. O PDF diz que essas etapas são cruciais na migração, porque **garantem a disponibilidade e a escalabilidade** do sistema.
- **Terceira aula**: o **volume** para as imagens do projeto, por meio de um projeto **CDN** que acessa um banco de dados, e um volume pelo arquivo de configuração.

## 1. Avalie o aplicativo
- Antes de migrar, analisar o aplicativo no IIS: **dependências, requisitos de sistema e configurações específicas**.
- Fazer uma **reunião com os times de infraestrutura e desenvolvimento** para levantar os **requisitos mínimos** da migração.
- Ao final, ter um **desenho** com as dependências e referências do projeto (**Figura 1 do PDF**, "Fluxo de projeto no IIS").

## 2. Crie uma imagem do Docker
- Um **Dockerfile** com todas as dependências e configurações, a partir de uma **imagem base apropriada para ASP.NET** (do site da Microsoft).
- Construir a imagem e guardá-la num **registro de contêineres**, como o **Amazon ECR** (Elastic Container Registry).
- **Testar o fluxo de criação dos contêineres**, criando os Pods para validar o comportamento. Com base na Figura 1, **criar um volume** e validar a aplicação com os volumes.

**Exemplo de Dockerfile para uma aplicação Node.js**
```dockerfile
# Imagem base com Node.js
FROM node:14
# Diretório de trabalho da aplicação
WORKDIR /usr/src/app
# Copia o package.json e o package-lock.json para o diretório de trabalho
COPY package*.json ./
# Instala as dependências do projeto
RUN npm install
# Copia os arquivos da aplicação para o diretório de trabalho
COPY . .
# Expõe a porta que a aplicação irá utilizar
EXPOSE 3000
# Comando para iniciar a aplicação
CMD [ "npm", "start" ]
```
Usa a imagem oficial do **Node.js 14**, define o diretório de trabalho, copia e instala as dependências, copia o resto dos arquivos, **expõe a porta 3000** e inicia com **`npm start`**. Ajuste a porta e os comandos para a sua aplicação.

## 3. Crie objetos do Kubernetes
| Objeto | Para quê | No exemplo |
|---|---|---|
| **Deployment** | Gerenciar a **implantação** do aplicativo | `my-nodejs-app`: **3 réplicas** da imagem `my-nodejs-app-image`, `containerPort: 3000` |
| **Service** | **Expor** o aplicativo na rede | `my-nodejs-app-service`: tipo **LoadBalancer**, mapeando a **porta 80** para a **3000** do contêiner (TCP) |
| **Ingress** (se necessário) | Configurar o **roteamento do tráfego externo** | `my-nodejs-app-ingress`: associa o domínio **`my-nodejs-app.example.com`** (path `/`, `pathType: Prefix`) ao `my-nodejs-app-service` na **porta 80** |

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nodejs-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nodejs-app
  template:
    metadata:
      labels:
        app: my-nodejs-app
    spec:
      containers:
      - name: my-nodejs-app
        image: my-nodejs-app-image
        ports:
        - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: my-nodejs-app-service
spec:
  selector:
    app: my-nodejs-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
  type: LoadBalancer
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-nodejs-app-ingress
spec:
  rules:
  - host: my-nodejs-app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-nodejs-app-service
            port:
              number: 80
```
> [!note] No PDF são três blocos separados. Aqui eles foram juntos com `---` e com a indentação refeita, porque a extração perdeu os recuos.

- Para subir os recursos no cluster EKS: o **kubectl**.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
