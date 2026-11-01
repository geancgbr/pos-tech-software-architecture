---
tags: [pos-tech/fase-2, terraform, revisao]
disciplina: Terraform
---

# Revisão - Terraform

[[Terraform]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- O que é o Terraform, e quem o desenvolve?
> Uma ferramenta de infraestrutura como código (IaC), da HashiCorp, para gerenciar, provisionar e orquestrar recursos em vários provedores de nuvem, data centers e outras plataformas, de forma declarativa. → [[TF 01 - Introdução ao Terraform]]

> [!question]- O que é IaC, e quais são os benefícios dela?
> Definir e gerenciar a infraestrutura por código, em vez de configurações manuais. Benefícios: automação, consistência, escalabilidade e rastreamento. → [[Infraestrutura como Código (IaC)]]

> [!question]- Cite ferramentas de IaC.
> Terraform, Ansible, Chef e CloudFormation.

> [!question]- O que é o HCL, e em quais ferramentas é usado?
> A HashiCorp Configuration Language: declarativa, legível e conversível para JSON. É usada no Terraform, no Nomad e no Consul. → [[HCL (HashiCorp Configuration Language)]]

> [!question]- Em `resource "aws_eks_cluster" "eks_cluster_fiap"`, o que é cada parte?
> `resource` é o tipo do bloco, `"aws_eks_cluster"` é o tipo de recurso e `"eks_cluster_fiap"` é o identificador.

## Aula 2 - Providers e backend
> [!question]- O que é um provider?
> Um plugin que implementa as APIs de uma plataforma e traduz o HCL em operações concretas. É o que torna o Terraform multicloud e agnóstico. → [[Providers do Terraform]]

> [!question]- Desde qual versão os providers são instalados automaticamente, e de onde?
> Desde o Terraform 0.13, a partir do HashiCorp Registry (ou de registries personalizados).

> [!question]- Cite boas práticas com providers.
> Fixar versões, nunca colocar credenciais no código (usar variáveis de ambiente ou o HashiCorp Vault), dividir em arquivos e módulos, e usar estado remoto.

> [!question]- O que é o tfstate?
> O arquivo JSON com o estado da infraestrutura gerenciada, a "verdade única". Contém IDs, atributos, dependências e metadata. → [[tfstate e Backend]]

> [!question]- Quais são os 4 passos de funcionamento do tfstate?
> Ler o estado, comparar com os arquivos de configuração, criar o plano e atualizar o estado.

> [!question]- O que é o bloqueio de estado, e onde ele existe?
> Um mecanismo que impede alterações simultâneas no estado. Existe em backends como o S3 (com DynamoDB) e o Terraform Cloud.

> [!question]- Backend local × remoto?
> Local (padrão): fácil e ideal para projetos pequenos, mas sem colaboração, sem bloqueio e com risco de perda. Remoto (recomendado): colaboração, criptografia, backups, bloqueio e acesso centralizado, mas exige configuração e depende de serviços externos.

## Aula 3 - Comandos
> [!question]- Qual é sempre o primeiro comando, e o que ele faz?
> `terraform init`: baixa os providers, configura o backend e verifica dependências e versões. → [[Comandos do Terraform]]

> [!question]- `plan` × `apply`?
> O `plan` gera e mostra o plano sem alterar a infraestrutura. O `apply` executa as mudanças, atualiza o tfstate e pede confirmação (a menos que se use `-auto-approve`).

> [!question]- Para que servem `-auto-approve`, `-var-file` e `-target`?
> Aplicar sem confirmação, informar um arquivo de variáveis e aplicar só recursos específicos.

> [!question]- Qual comando sincroniza o estado depois de mudanças feitas fora do Terraform?
> `terraform refresh`.

> [!question]- Qual comando traz para o Terraform recursos criados fora dele?
> `terraform import`.

> [!question]- O que o `terraform graph` gera?
> Um gráfico de dependências em formato DOT, visualizável com o Graphviz (que precisa ser instalado).

> [!question]- O que o `terraform state` permite?
> Manipular o estado diretamente (`mv`, `rm`, `list`) sem alterar a infraestrutura.

## Aula 4 - Variáveis e output
> [!question]- Quais são os três tipos de variáveis?
> De entrada (`variable`), de saída (`output`) e locais (`locals`). → [[Variáveis, Outputs e Locals no Terraform]]

> [!question]- Como se referencia uma variável de entrada?
> `var.nome-var`.

> [!question]- Cite os tipos simples e complexos.
> Simples: string, number e bool. Complexos: list, map, set, object e tuple.

> [!question]- Quais arquivos de variáveis o Terraform busca automaticamente?
> `terraform.tfvars` e `*.auto.tfvars`.

> [!question]- Qual é o prefixo das variáveis de ambiente?
> `TF_VAR_`.

> [!question]- O que acontece se a variável não tiver default nem valor informado?
> O Terraform pede o valor interativamente.

> [!question]- Para que serve `sensitive = true`?
> Para que senhas e chaves não apareçam em logs nem na saída.

> [!question]- Como restringir os valores permitidos numa variável?
> Com um bloco `validation` (condition e error_message).

## Aula 5 - Data e locals
> [!question]- O que é um data source?
> Um bloco `data` que consulta informações de recursos existentes, sem criar nem alterar nada (somente leitura). → [[Data Sources no Terraform]]

> [!question]- Quando os data sources são consultados?
> Em tempo de execução: o PDF diz que o primeiro passo acontece no `plan` e `apply`, e cita a fase de planejamento (`terraform plan`).

> [!question]- Como se acessa um local, e ele pode mudar em execução?
> Com `local.<nome>`. É imutável: não muda em tempo de execução.

> [!question]- Data sources × locals?
> Os data sources consultam e integram dados externos. Os locals estruturam e derivam valores internos.

## Aula 6 - Módulos
> [!question]- O que é um módulo?
> A unidade de organização e reutilização da IaC: um agrupamento lógico de recursos, variáveis e saídas. → [[Módulos do Terraform]]

> [!question]- Quais são os arquivos básicos de um módulo?
> `main.tf`, `variables.tf` e `outputs.tf`.

> [!question]- Módulo local × remoto?
> Local: um diretório do projeto (`source = "./modulos/ec2"`). Remoto: ex.: Terraform Registry. O Código-fonte 1 da aula usa `terraform-aws-modules/ec2-instance/aws`.

> [!question]- Cite boas práticas com módulos.
> Fixar versão, criar módulos simples, testar isoladamente, documentar, evitar hardcoding e validar periodicamente.

## Aula 7 - Loops e expressões
> [!question]- `count` × `for_each`?
> count: um número inteiro, para o mesmo recurso várias vezes com a mesma configuração; as instâncias são referenciadas pelo índice. for_each: lista ou mapa, para recursos com configurações diferentes; usa `each.key` e `each.value`. → [[Loops e Expressões no Terraform]]

> [!question]- O que é uma expressão no Terraform?
> Um trecho de código que retorna um valor.

> [!question]- Cite funções do Terraform citadas na aula.
> `length()`, `join()`, `lookup()` e `element()`.

## Aula 8 - EKS
> [!question]- O que é o EKS?
> O serviço gerenciado pela AWS para executar clusters Kubernetes. → [[EKS (Elastic Kubernetes Service)]]

> [!question]- Quais recursos a aula cria para o cluster EKS?
> Provider AWS, VPC (com subnets pública e privada e internet gateway), duas roles IAM (cluster e node group), o cluster, o node group, o controle de acesso (access entry e policy association) e o output kubeconfig.

> [!question]- Para que servem as duas roles IAM?
> A do cluster dá permissões para o EKS criar e gerenciar recursos. A do node group permite que os nós interajam com o EKS e com serviços como o ECR.

> [!question]- O que é um Node Group?
> As instâncias EC2 que executam os workloads do Kubernetes.

> [!question]- Como verificar os nós depois do apply?
> Com `kubectl get nodes` (e no AWS Management Console, em EKS).

## Aula 9 - Terraform Cloud
> [!question]- Qual é a principal característica do Terraform Cloud?
> O gerenciamento de estado remoto. Ele também oferece bloqueio de estado. → [[Terraform Cloud]]

> [!question]- Para que servem os workspaces?
> Para representar ambientes ou projetos (dev, teste, produção), cada um com suas configurações e variáveis.

> [!question]- O que é o RBAC no Terraform Cloud?
> O controle de acesso por funções: membros diferentes podem executar, revisar ou aprovar.

> [!question]- Com quais ferramentas de CI/CD ele integra?
> Jenkins, GitLab CI, GitHub Actions e CircleCI.

> [!question]- Terraform Cloud × Terraform Enterprise?
> O Cloud é SaaS, com funcionalidades gratuitas ou planos para pequenas e médias empresas. O Enterprise tem suporte dedicado, audit logs e integração empresarial, e pode ser hospedado na nuvem ou on-premises.

## Dúvidas em aberto
- [ ] **`locals.` × `local.`**: o exemplo da aula 4 usa `locals.instanceType`, e a aula 5 diz que o acesso é por `local.<nome>`.
- [ ] **`source = "hashicorpo/aws"`** (aula 2): está grafado assim no PDF.

## Pontos fracos (o que errei)
<!-- anote aqui as perguntas que errou, com a data -->
