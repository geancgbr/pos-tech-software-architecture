---
tags: [pos-tech/fase-2, terraform, aula]
disciplina: Terraform
aula: 5
fonte: "POSTECH - Aula5_rev2.pdf"
---

# TF 05 - Data e locals

← [[TF 04 - Variáveis e output]] · [[Terraform]] · Próxima → [[TF 06 - Módulos]]

> [!summary] Em uma frase
> O **[[Data Sources no Terraform|data source]]** (`data`) **consulta** informações de recursos que já existem, sem criar nem alterar nada. Os **locals** definem valores **imutáveis** (constantes ou derivados) para evitar repetição, acessados com `local.<nome>`.

## Hands On
Buscar informações de recursos na nuvem com o bloco **Data** e usar **Locals**.

## Data sources
- Acessam informações de infraestrutura gerenciada por provedores, **sem recriar nem modificar** os recursos. São úteis para recursos criados **fora do Terraform** ou **por outros módulos**.
- **De onde vêm os dados**: recursos em provedores (AWS, Azure, GCP, OCI...), **APIs públicas** e infraestrutura de outras ferramentas ou equipes.
- **Características**: **somente leitura** e **dinamismo** (dependências dinâmicas entre recursos e dados externos).

```hcl
data "<provider>_<resource_type>" "<name>" {
  # Argumentos necessários para filtrar ou localizar o recurso
}

data "aws_iam_role" "labrole" {
  name = "LabRole"
}
```
`<provider>` (ex.: aws, google) · `<resource_type>` (ex.: ami, vpc) · `<name>` (identificador interno).

**Exemplo: a AMI mais recente**, sem procurar no console:
```hcl
data "aws_ami" "latest_amazon_linux" {
  most_recent = true
  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
  owners = ["137112412989"] # AWS ID oficial para AMIs da Amazon
}

resource "aws_instance" "example" {
  ami           = data.aws_ami.latest_amazon_linux.id
  instance_type = "t2.micro"
}
```
1. O Terraform consulta a **API da AWS** com o filtro.
2. Seleciona a mais recente (`most_recent`).
3. Disponibiliza o ID em `data.aws_ami.latest_amazon_linux.id`.

- Os data sources são consultados na fase de **planejamento** (`terraform plan`), para os valores estarem resolvidos antes do apply.
- Podem ter **dependências**, por exemplo buscar uma sub-rede que depende de uma VPC gerenciada pelo Terraform.

## Locals
- Valores **locais**, constantes ou derivados, que **simplificam** a configuração e **evitam repetir expressões complexas**. Funcionam como **variáveis somente leitura**, calculadas uma vez.
- Podem ser simples (strings, números) ou complexos (mapas, listas).
- **Acesso**: `local.<nome>` (ex.: `local.tags`). **É imutável**: não muda em tempo de execução.

```hcl
resource "aws_security_group" "sg" {
  name        = "SG-${var.projectName}"
  description = "Este grupo e usado na live de terraform"
  vpc_id      = data.aws_vpc.vpc.id
  # no PDF: um bloco ingress (from_port/to_port 80, protocol "tcp") e um egress (from_port/to_port 0, protocol "-1"), ambos com cidr_blocks ["0.0.0.0/0"]
  tags = local.tags
}
```

**Boas práticas com locals**
1. **Não abuse**: o excesso dificulta a leitura.
2. **Centralize** cálculos e lógica repetitiva.
3. **Nomes claros**.
4. **Imutabilidade**: o valor é fixo depois de definido.

**Em resumo**: os **data sources** consultam e integram **dados externos**, e os **locals** estruturam e derivam **valores internos**.

## Referências
HashiCorp: Locals, Data sources, Resource Dependencies
