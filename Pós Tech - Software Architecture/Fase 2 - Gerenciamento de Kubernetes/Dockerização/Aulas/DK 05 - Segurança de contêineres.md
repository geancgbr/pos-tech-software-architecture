---
tags: [pos-tech/fase-2, docker, aula]
disciplina: Dockerização
aula: 5
fonte: "Aula 05- Segurança de Contêineres.pdf"
---

# DK 05 - Segurança de contêineres

← [[DK 04 - Melhores práticas e solução de problemas]] · [[Dockerização]] · Próxima → [[DK 06 - ECS]]

> [!summary] Em uma frase
> A análise de vulnerabilidades de imagens Docker é feita localmente com o **[[Trivy]]** (open source). Uma forma de **reduzir as vulnerabilidades** é escolher **imagens base mais enxutas**, como a variação **alpine**.

## Hands On
Analisar as vulnerabilidades de uma imagem e resolvê-las com imagens menores, que vêm com menos funcionalidades pré-instaladas.

## Por que analisar
Ferramentas assim ajudam a **identificar e corrigir vulnerabilidades**, para que a aplicação não tenha brechas expostas a pessoas mal-intencionadas. Também ajudam a entender melhor o Docker e a criar **imagens cada vez mais seguras**.

## Trivy: instalação no WSL (Ubuntu)
```bash
# download e extração
wget https://github.com/aquasecurity/trivy/releases/download/v0.48.0/trivy_0.48.0_Linux-64bit.tar.gz && tar -xzf trivy_0.48.0_Linux-64bit.tar.gz

# mover para o diretório binário do Linux
sudo mv trivy /usr/local/bin/

# conferir a instalação
trivy version
```

## Fazendo o scan
1. Faça o build da imagem com uma **tag**, usando a flag **`-t`** (o Dockerfile de exemplo está na Figura 1 e o build, na Figura 2). No exemplo, a tag é **`teste-trivy:latest`**.
2. Rode a análise:

```bash
trivy image teste-trivy:latest
```

A saída pode ser **muito extensa**. Por padrão, mostra todos os níveis de severidade:

| Nível | Significado |
|---|---|
| **Unknown** | Desconhecido (severidade ainda não definida) |
| **Low** | Baixo |
| **Medium** | Médio |
| **High** | Alto |
| **Critical** | Crítico |

3. Para filtrar, use **`--severity`** com um ou mais níveis:

```bash
trivy image --severity CRITICAL,HIGH teste-trivy:latest
```

Com muitas vulnerabilidades, dá para olhar **só o CRITICAL** (Figura 4).

## Lendo o resultado
- A coluna **"Title"** traz um **link** para uma página com detalhes da vulnerabilidade (**Aqua Vulnerability Database**, Figura 5).
- **Exemplo**: a biblioteca **openssl-client** da imagem **node:18**. O componente **ssh-add do OpenSSH, antes da versão 9.3**, adiciona chaves de Smartcard ao ssh-agent **sem restrições**. Ou seja, a node:18 tem um OpenSSH anterior à 9.3, que ainda tem esse problema.

## Como reduzir as vulnerabilidades
Escolha **imagens base mais enxutas**, com menos pacotes e funcionalidades, que muitas vezes a aplicação nem usa. No exemplo, a mesma versão do Node (18) na variação **alpine**, que além de **bem menor** não teve **nenhuma vulnerabilidade** (Figura 6).

## Referências
Aqua Vulnerability Database, *CVE-2023-28531* · TrendMicro, *O que é Segurança de Contêineres Docker?* · Medium, *Scanning Docker Images for Vulnerabilities using Trivy* · *Trivy Documentation* (v0.48)
