---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 3
fonte: "POSTECH - Aula3_rev2.pdf"
---

# TF 03 - Principais comandos

← [[TF 02 - Providers e backend]] · [[Terraform]] · Próxima → [[TF 04 - Variáveis e output]]

> [!summary] Em uma frase
> Os [[Comandos do Terraform|comandos]] cobrem o ciclo de vida da IaC: **init → validate → plan → apply → destroy**, mais `show`, `output`, `refresh`, `state`, `fmt`, `graph` e `import`.

## Hands On (vídeos)
Criar um arquivo de **bucket S3** e testar os principais comandos.

## Os comandos
| Comando | O que faz | Quando usar |
|---|---|---|
| **`terraform init`** | **Sempre o primeiro.** Inicializa o diretório: baixa os **providers**, configura o **backend** (local ou remoto) e verifica dependências e versões | Diretório novo; depois de adicionar ou mudar um provider no `main.tf`; quando o backend muda |
| **`terraform validate`** | Verifica **sintaxe e estrutura** dos `.tf` (HCL e regras dos providers). Erros apontam a linha ou o bloco | Depois de criar ou mudar arquivos `.tf`, antes de aplicar |
| **`terraform plan`** | Gera e mostra o **plano de execução**, **sem alterar nada**: compara o tfstate com os `.tf` e lista "create", "update" ou "destroy" | **Sempre antes de aplicar**; para compartilhar planos em equipe |
| **`terraform apply`** | **Executa o plano**: provisiona, modifica ou destrói, **atualiza o tfstate** e **pede confirmação** (a menos que se use `-auto-approve`) | Depois de revisar o plan |
| **`terraform show`** | Exibe o **estado** (recursos, atributos, valores) sem abrir o tfstate | Ver o estado atual; depuração |
| **`terraform destroy`** | Identifica os recursos no tfstate e os destrói de forma **segura e ordenada**, pedindo confirmação | Desmontar ambientes de teste; antes de reconfigurar tudo |
| **`terraform output`** | Lê o tfstate e retorna os valores dos blocos **`output`** | Compartilhar informações (IPs, nomes de buckets) com outras equipes; depuração |
| **`terraform refresh`** | Compara o estado com a infraestrutura **real** e atualiza o tfstate | Quando houve mudanças **fora do Terraform** |
| **`terraform state`** | Manipula o estado diretamente (`mv`, `rm`, `list`) **sem alterar a infraestrutura** | Estado corrompido; refatorar, movendo recursos entre módulos |
| **`terraform fmt`** | **Formata** o código (indentação, espaçamento, organização) | Depois de escrever ou modificar `.tf` |
| **`terraform graph`** | Gera um gráfico das **dependências** em formato **DOT**, visualizável com o **Graphviz** (que precisa ser instalado), com saída em PNG | Entender a ordem de criação; mapear dependências complexas |
| **`terraform import`** | Traz para o Terraform **recursos criados fora dele** e atualiza o estado | Migrar recursos existentes; integrar infraestrutura legada |

**Parâmetros úteis**
- `apply`: **`-auto-approve`** (sem confirmação) · **`-var-file`** (arquivo de variáveis) · **`-target`** (só alguns recursos).
- `destroy`: **`-target`** · **`-auto-approve`**.

**Exemplo de output**:
```hcl
output "bucket_arn" {
  value = aws_s3_bucket.backend-tf.arn
}
```

As saídas de cada comando estão nas Figuras 1 a 13 do PDF.

## Referências
HashiCorp: Provisionando infraestrutura com Terraform, Terraform resource, Terraform import
