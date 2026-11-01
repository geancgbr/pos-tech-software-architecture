---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 7
fonte: "Kubernetes parte 2/Aula 7.pdf (Thiago Adriano)"
---

# K8S2 07 - Kubernetes CI-CD

← [[K8S2 06 - AWS EKS na prática, parte 2]] · [[Kubernetes]] · Próxima → [[K8S2 08 - Segurança do AWS EKS]]

> [!summary] Em uma frase
> Uma **esteira de CI/CD** com **Git, Azure DevOps e Kubernetes**: os projetos são **construídos automaticamente** a cada alteração, **testados** em diferentes ambientes e **implantados em produção** de forma automatizada. Segundo o resumo, a esteira foi **integrada com o EKS da AWS**.

## Hands On
Criar uma esteira de desenvolvimento e deploy com CI/CD no **Azure DevOps**. Benefícios mostrados: **redução de erros e atrasos na entrega**, e a integração e a entrega contínuas **acelerando o desenvolvimento** e aumentando a eficiência.

## Contexto
- As empresas precisam entregar software **rápido e com eficiência**, sem comprometer **qualidade ou segurança**. Para isso, é preciso **automatizar** o processo de entrega, da integração à implantação em produção.
- Com a esteira configurada, os projetos são **construídos automaticamente** sempre que o código muda, **testados em diferentes ambientes** e **implantados em produção automaticamente**.

## CI: Integração Contínua
- O processo de **integrar as alterações ao projeto principal com frequência**, geralmente **várias vezes ao dia**, para **detectar e corrigir problemas rapidamente**, antes que fiquem maiores. Ver [[Integração Contínua (CI)]].

**YAML de exemplo (projeto Node.js)**
```yaml
# Define o nome do pipeline e onde ele deve rodar
name: Node.js CI
on:
  push:
    branches: [main]
jobs:
  # Define o job de build
  build:
    runs-on: ubuntu-latest
    steps:
      # Clona o repositório do Git
      - name: Checkout
        uses: actions/checkout@v2
      # Instala as dependências do projeto
      - name: Install Dependencies
        run: npm install
      # Executa os testes
      - name: Run Tests
        run: npm test
```
O pipeline **"Node.js CI"** roda **a cada push na branch `main`**. O job **"build"** roda numa VM **Ubuntu** e tem três etapas: **clonar o repositório**, **instalar as dependências** e **executar os testes automatizados**.

## CD: Implantação Contínua (ou Entrega Contínua)
- O processo de **implantar as alterações de forma automatizada** em ambientes de **teste e produção**, entregando aos usuários **mais rápido e com segurança**. Ver [[Entrega Contínua e Deploy Contínuo]].

**YAML de exemplo (Node.js no Azure, multistage com 3 ambientes)**
| Step | Condição (`if`) | `app-name` | `slot-name` | `publish-profile` |
|---|---|---|---|---|
| Deploy to Development | `github.ref == 'refs/heads/main'` | `my-node-app-dev` | `dev` | `secrets.DEV_PUBLISH_PROFILE` |
| Deploy to Staging | `github.ref == 'refs/tags/*'` | `my-node-app-staging` | `staging` | `secrets.STAGING_PUBLISH_PROFILE` |
| Deploy to Production | `github.ref == 'refs/heads/release'` | `my-node-app-prod` | `production` | `secrets.PRODUCTION_PUBLISH_PROFILE` |

- O pipeline **"Node.js CD"** tem `trigger` com `branches: include: - main`. Segundo o texto, roda a cada push na **`main`**.
- O job **"deploy"** roda numa VM **Ubuntu**: faz o checkout (`actions/checkout@v2`) e configura os três ambientes (**desenvolvimento, homologação e produção**).
- Cada ambiente usa o **`Azure/webapps-deploy@v2`**, que o PDF descreve como **"uma ação do GitHub"** para implantar num **Web App do Azure**. Cada um tem nome de aplicativo, **slot** e **perfil de publicação** próprios, todos com `package: './dist'`.
- Dá para personalizar o pipeline com etapas de **build, teste e empacotamento** antes de cada ambiente.

> [!note] O texto fala em **Azure DevOps**, mas os dois YAML usam elementos de GitHub Actions (`runs-on`, `uses: actions/checkout@v2`, `github.ref`), e o próprio PDF chama o `webapps-deploy@v2` de "ação do GitHub". O YAML do CD mistura `trigger` com `jobs`/`steps`. Está assim no PDF.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
