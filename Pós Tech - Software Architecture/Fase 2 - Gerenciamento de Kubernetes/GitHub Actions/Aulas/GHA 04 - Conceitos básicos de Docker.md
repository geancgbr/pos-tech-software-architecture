---
tags: [pos-tech/fase-2, github-actions, aula]
disciplina: GitHub Actions
aula: 4
fonte: "Aula 04 - Conceitos básicos de Docker.pdf"
---

# GHA 04 - Conceitos básicos de Docker

← [[GHA 03 - GitHub Actions em ambientes On-Premises]] · [[GitHub Actions]] · Próxima → [[GHA 05 - Repositório de imagens Docker]]

> [!summary] Em uma frase
> O [[Docker]] é uma **plataforma aberta** para criar, empacotar e executar aplicativos em **[[Contêiner|contêineres]]**, que funcionam igual em qualquer ambiente. Isso acaba com o "funciona na minha máquina". A **imagem** é o modelo, e o **contêiner** é a imagem em execução.

## Hands On: instalação
- **Windows**: baixar e instalar o **Docker Desktop for Windows** e reiniciar, se necessário.
- **Mac**: baixar e instalar o **Docker Desktop for Mac**.
- **Linux (Ubuntu)**:

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce
```

## Por que Docker
- Desenvolver e implantar ficou complexo: **compatibilidade, dependências e diferenças entre os ambientes** de desenvolvimento e produção.
- **Contêiner**: um pacote **leve e independente** com tudo de que o app precisa (código, bibliotecas, variáveis de ambiente...). Os contêineres são **isolados** entre si e funcionam igual onde forem implantados.
- **Fim do "funciona na minha máquina"**: o app e as dependências encapsulados rodam igual em qualquer ambiente.
- **Eficiência**: os contêineres **compartilham o kernel do SO**, mas mantêm processos e arquivos separados. Muitos rodam numa única máquina, **sem o overhead de uma VM completa**.
- Acelera a entrega: empacotar, distribuir e executar de forma rápida e confiável, com ambientes replicados de forma consistente.

## Imagens e contêineres
| | Imagem | Contêiner |
|---|---|---|
| O que é | Pacote **leve, autônomo e executável** com código, bibliotecas, variáveis de ambiente e configurações | **Instância executável** de uma imagem: "a imagem em tempo de execução" |
| Natureza | **Modelo estático** | **Execução viva** do modelo |
| Detalhes | Composta por **camadas**, uma por instrução do Dockerfile, empilhadas e **cada uma dependendo da anterior**. Camadas comuns são compartilhadas entre imagens | Pode ser iniciado, parado, movido ou excluído pela **API ou pela CLI** do Docker. Interage direto com o kernel, mas fica separado dos outros processos |
| Onde fica | Em **repositórios**, como o **Docker Hub** (públicas ou privadas) | Não citado (os contêineres isolam o software da máquina host e de outros contêineres) |

## Casos de uso
- **Desenvolvimento e teste**: ambientes idênticos ao de produção.
- **CI/CD**: automatizar compilação, teste e implantação nos pipelines.
- **Microsserviços**: serviços independentes que trabalham juntos, com mais escalabilidade e resiliência.
- **Orquestração**: com ferramentas como o **Kubernetes**, gerenciar e escalar contêineres conforme a carga.

## Impacto na indústria
**Padronização** · **agilidade e eficiência** · **inovação em infraestrutura** (orquestração, monitoramento, segurança) · **ecossistema próspero** · **sustentabilidade** (melhor uso do hardware e eficiência energética).

**Para continuar**: documentação oficial · Docker Hub · comunidade Docker · livros e blogs.

> [!note] O fechamento diz que o material explorou "repositórios de imagens" e "considerações de segurança". Repositórios são só citados de passagem nesta aula (Docker Hub), e as considerações de segurança não aparecem: os dois temas são tratados na **aula 5**.

## Referências
AWS, *O que é o Docker?* · Docker, *Develop faster. Run anywhere.* · Microsoft, *O que é o Docker?* · Red Hat, *Docker: desenvolvimento de aplicações em containers*
