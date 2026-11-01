---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 1
fonte: "Aula 01- Introdução ao Docker.pdf"
---

# DK 01 - Introdução ao Docker

[[Dockerização]] · Próxima → [[DK 02 - Gerenciamento de contêineres]]

> [!summary] Em uma frase
> O [[Docker]] (dotCloud, 2013, open source) roda aplicações em [[Contêiner|contêineres]] isolados e com recursos controlados, graças ao isolamento de processos e à virtualização do Kernel Linux, e a duas tecnologias que atuam junto do Kernel: [[Cgroups e Namespaces|Cgroups]] (limites de recursos) e **Namespaces** (isolamento). Os contêineres nascem de [[Imagens Docker e Docker Hub|imagens]], descritas num **Dockerfile**.

## Hands On
Instalação do **WSL** (subsistema Linux no Windows) via PowerShell, do **Docker Desktop** integrado ao WSL e o primeiro contêiner. Os comandos Docker são executados no ambiente Linux.

## Docker e o Kernel Linux
- Lançado em **2013** pela empresa **dotCloud**. É uma ferramenta **open source** criada para **melhorar o isolamento e o uso de recursos** e rodar aplicações **sem interface gráfica**, em comparação com uma **VM**.
- Só existe porque o **Kernel do Linux** permite **isolar processos** e **virtualização**.
- **Kernel** quer dizer "núcleo" e é o principal componente do Linux: a interface central entre o hardware e os processos, que gerencia os recursos com eficiência. **Funções**: gerenciar memória, processos, drives, chamadas do sistema e segurança.

## Cgroups e Namespaces
| | Cgroups | Namespaces |
|---|---|---|
| Para quê | Definir **limites de uso de recursos** dos processos | Criar **isolamentos** transparentes e lógicos |
| O que permite | Limitar CPU e memória (com um único comando); priorizar processos; controlar quais podem ser reiniciados, interrompidos ou congelados | Cada contêiner com seus próprios usuários, rede, disco etc.; contêineres diferentes rodando em paralelo no mesmo servidor |
| No contêiner | Controla os processos em execução, essencial para funcionar sem gargalos | Se um contêiner quebra (ex.: usa 100% da CPU), os outros não são afetados |

> [!example] Analogia do navio cargueiro
> Se um contêiner cai no mar, os outros não são afetados, nem o navio, que representa o **host** onde os contêineres rodam (Figura 2 do PDF).

As diferenças entre **VMs e contêineres** "são poucas, mas mudam completamente o modo de execução e isolamento das aplicações". As comparações estão nas Figuras 3 e 4 do PDF; o texto não detalha as diferenças.

## Imagens, Docker Hub e tags
- **Imagens** empacotam o **sistema operacional, as dependências, as portas expostas e as variáveis de ambiente**. Há milhares prontas, e você pode criar a sua e compartilhar.
- **Exemplo**: para uma aplicação NodeJS seria preciso instalar a versão certa do Node, as dependências (NPM/YARN) e a configuração padrão. As imagens personalizadas cumprem esse papel.
- **Docker Hub** é "um GitHub voltado para imagens Docker": imagens **oficiais** e **não oficiais** (da comunidade), públicas ou privadas. Você baixa com **"pull"**, pela URL e pela tag.
- **Tags** definem a **versão da imagem**, para controle, atualização e organização: correção de bugs, melhorias e correções de segurança.

## Dockerfile
É o arquivo onde se declaram os comandos, as instalações, as variáveis e as portas de uma imagem personalizada. **O nome do arquivo já é a sua extensão.** O PDF mostra um **Dockerfile simples** (Figura 5) e um **Dockerfile multistage** (Figura 6). Veja [[Dockerfile e Camadas (Layers)]].

## Referências
Microsoft Learn, *Como instalar o Linux no Windows com o WSL* (2023) · ETCD.DEV, *Containers: o que são namespaces e cgroups* (2021) · Red Hat, *O que é o Kernel Linux* (2019)
