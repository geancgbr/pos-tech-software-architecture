---
tags: [pos-tech/fase-2, terraform, conceito]
aliases: [tfstate, terraform.tfstate, State, Estado do Terraform, Backend, Back-end remoto, Bloqueio de estado]
---

# tfstate e Backend

**tfstate**: o arquivo **JSON** que guarda o estado da infraestrutura gerenciada, a **"verdade única"** do que foi criado, atualizado ou destruído. É gerado quando comandos como `apply` ou `destroy` são executados e contém IDs, atributos, **dependências** e metadata.

**Ciclo**: ler o estado → comparar com o HCL → gerar o plano → atualizar o estado.

**Cuidados**: **backups regulares** e backend remoto seguro · **bloqueio de estado** (S3 com DynamoDB, Terraform Cloud) para evitar alterações simultâneas.

**Backend**: a interface que gerencia o estado (armazenamento, bloqueio, execução remota).

| | Local (padrão) | Remoto (recomendado) |
|---|---|---|
| Onde | `terraform.tfstate` no diretório | S3, Azure Blob, Google Cloud Storage, Terraform Cloud |
| Prós | Fácil; projetos pessoais ou pequenos | Colaboração, criptografia, backups, **bloqueio**, acesso centralizado |
| Contras | Sem colaboração, risco de perda, sem bloqueio | Configuração inicial; dependência externa |

Exemplo de backend S3: [[TF 02 - Providers e backend#Backend]]. No [[Terraform Cloud]], o estado remoto é a principal característica, e ele também oferece bloqueio de estado.
