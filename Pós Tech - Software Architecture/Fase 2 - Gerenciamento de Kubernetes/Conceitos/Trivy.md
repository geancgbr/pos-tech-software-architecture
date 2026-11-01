---
tags: [pos-tech/fase-2, docker, conceito, seguranca]
aliases: [Trivy scan, Análise de vulnerabilidades de imagens]
---

# Trivy

Ferramenta **open source** para **analisar as vulnerabilidades de imagens Docker localmente**.

- **Instalação no WSL/Ubuntu**: `wget` do release v0.48.0 + `tar -xzf`, `sudo mv trivy /usr/local/bin/` e `trivy version`.
- **Scan**: `trivy image <imagem:tag>`, com a imagem construída com `-t`.
- **Severidades**: Unknown · Low · Medium · High · Critical. Para filtrar, `--severity CRITICAL,HIGH`.
- A coluna **Title** traz um link para a **Aqua Vulnerability Database**. Exemplo: o OpenSSH anterior à 9.3 na node:18 (o ssh-add adiciona chaves de Smartcard ao ssh-agent sem restrições).
- **Para reduzir as vulnerabilidades**: imagens base **enxutas**, como a **alpine** (a imagem do Node 18 na variação alpine não teve nenhuma).

Comandos completos: [[DK 05 - Segurança de contêineres]]
