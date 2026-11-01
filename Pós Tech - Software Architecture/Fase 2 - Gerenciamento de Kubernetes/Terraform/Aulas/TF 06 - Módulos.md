---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 6
fonte: "POSTECH - Aula6_rev2.pdf"
---

# TF 06 - Módulos

← [[TF 05 - Data e locals]] · [[Terraform]] · Próxima → [[TF 07 - Loops e expressões]]

> [!summary] Em uma frase
> Os **[[Módulos do Terraform|módulos]]** são a unidade de **organização e reutilização** da IaC. Encapsulam recursos, variáveis e saídas (`main.tf`, `variables.tf`, `outputs.tf`) e podem ser **locais** ou **remotos** (Terraform Registry).

## Hands On (vídeos)
Criar um módulo e usá-lo para montar uma infraestrutura completa na AWS.

## O que são
- **Definição**: um agrupamento lógico de recursos (um ou vários) que representa uma funcionalidade, como redes, instâncias EC2 ou bancos de dados.
- **Modularidade**: como funções nas linguagens de programação, evitam duplicação.
- **Flexibilidade**: **locais** (diretórios do projeto) ou **remotos** (ex.: Terraform Registry). Há módulos da HashiCorp, da comunidade ou os seus, que podem ser publicados num repositório público do GitHub.
- **Por que usar**: menos duplicação · mais legibilidade e organização · mais colaboração.

**Exemplo do Código-fonte 1** (`terraform-aws-modules/ec2-instance/aws`; nas Referências do PDF esse módulo aparece como "AWS EC2 Module. Terraform Registry"):
```hcl
module "ec2_instance" {
  source                 = "terraform-aws-modules/ec2-instance/aws"
  name                   = "single-instance"
  instance_type          = "t2.micro"
  key_name               = "user1"
  monitoring             = true
  vpc_security_group_ids = ["sg-12345678"]
  subnet_id              = "subnet-eddcdzz4"
  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}
```

## Estrutura e funcionamento
- **`main.tf`**: os recursos e a lógica. **`variables.tf`**: as variáveis de entrada. **`outputs.tf`**: as saídas consumidas por outros.
- **Fluxo**:
  1. Escreve-se o módulo.
  2. O arquivo principal o chama com os valores das variáveis.
  3. No `terraform apply`, o Terraform processa o módulo e aplica os recursos.

**Exemplo de módulo local** (`/modulos/ec2`):
```hcl
resource "aws_instance" "web" {
  ami           = var.ami
  instance_type = var.instance_type
  tags = {
    Name = var.name
  }
}

variable "ami" {}
variable "instance_type" {}
variable "name" {}
```
**Chamando o módulo**, de outro diretório:
```hcl
module "web_instance" {
  source        = "./modulos/ec2"
  ami           = "ami-12345678"
  instance_type = "t2.micro"
  name          = "Servidor Web"
}
```

## Benefícios
| Benefício | Exemplo ou ideia |
|---|---|
| **Reutilização** | Um módulo de VPC usado em produção, desenvolvimento e teste |
| **Padronização** | Políticas de segurança, naming conventions, boas práticas |
| **Redução de erros** | Testado uma vez e reaplicado com confiança |
| **Escalabilidade** | Evita que o projeto fique monolítico |
| **Documentação e manutenção** | Menos dependência de pessoas específicas |

## Boas práticas
1. **Versionamento**: fixe a versão dos módulos remotos.
2. **Módulos simples**: um objetivo específico por módulo.
3. **Teste isoladamente** antes de integrar.
4. **Documente** variáveis, saídas e objetivo, com exemplos.
5. **Evite hardcoding**: tudo o que for personalizável vira variável.
6. **Valide periodicamente** com `terraform validate`.

O resumo da aula lembra que dá para deixar **valores default dentro do módulo**, para reduzir o que é preciso informar ao chamá-lo.

## Referências
Terraform Registry (AWS EC2 Module) · HashiCorp: Module create, Modules overview
