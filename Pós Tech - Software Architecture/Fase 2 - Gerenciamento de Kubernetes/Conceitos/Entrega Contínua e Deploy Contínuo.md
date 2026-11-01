---
tags: [pos-tech/fase-2, devops, conceito]
aliases: [CD, Entrega Contínua, Deploy Contínuo, Continuous Delivery, Continuous Deployment, Pequenos lotes]
---

# Entrega Contínua e Deploy Contínuo

O **CD** do "CI/CD" engloba **dois processos**:

| | Entrega contínua | Deploy contínuo |
|---|---|---|
| O que garante | Cada mudança **pode** ir para produção | Cada pacote **vai** para produção automaticamente |
| Intervenção humana | A equipe pode optar por **não implantar**, geralmente por **motivos comerciais** | **Nenhuma**: implanta assim que cumpre todos os requisitos da esteira (qualidade, segurança...) |
| Pacote | Pronto, testado e guardado num **repositório de artefatos** | Implantado |

**Para haver deploy contínuo, é preciso ter entrega contínua.**

**Pequenos lotes**
- Trabalha-se em grandes lotes por causa do **custo fixo alto** de entregar.
- A entrega contínua torna **viável** trabalhar em pequenos lotes: feedback mais rápido, triagem e correção mais fáceis, mais eficiência e motivação, e sem cair na **falácia do custo irrecuperável**.
- Também **reduz o risco** da mudança.

## Na disciplina GitHub Actions (aula 1): "distribuição contínua"
A aula chama a entrega contínua também de **distribuição contínua**: uma **evolução lógica da CI**, em que as alterações são automaticamente preparadas e implementadas num ambiente de **teste e/ou produção** depois da compilação, com sempre **um artefato validado e pronto para implantação**. Automatiza testes além dos de unidade (**IU, carga, integração, confiabilidade de API**), e a nuvem barateou criar ambientes de teste.

## Na disciplina Kubernetes (parte 2, aula 7)
A aula traduz **CD** como **"Implantação Contínua" (ou "Entrega Contínua")**: o processo de **implantar as alterações de forma automatizada** em ambientes de teste e produção. O exemplo ("Node.js CD") implanta em **três ambientes** no Azure (desenvolvimento, homologação e produção) com o `Azure/webapps-deploy@v2`. → [[K8S2 07 - Kubernetes CI-CD]]

Aparece em: [[DEV 01 - CI-CD principais conceitos]], [[GHA 01 - Introdução]], [[K8S2 07 - Kubernetes CI-CD]]
