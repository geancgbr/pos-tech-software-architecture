---
tags: [pos-tech/fase-4, banco-de-dados, cloud, aula]
disciplina: Data Engineering
aula: 6
fonte: "Data Engineering/10SOAT - Fase 4 - Data engineering - Aula 06.pdf"
---

# DE 06 - Cloud e DBaaS

← [[DE 05 - Bancos orientados a grafos com Neo4j]] · [[Data Engineering]] · Próxima → [[DE 07 - Bancos de dados e microsserviços]]

> [!summary] Em uma frase
> **Cloud computing** é o acesso **sob demanda** a recursos de TI compartilhados pela internet, alugados de provedores, nos modelos **IaaS, PaaS e SaaS**. O **[[DBaaS (Database-as-a-Service)|DBaaS]]** aplica a cloud aos bancos de dados: o provedor entrega um banco **gerenciado**. Na **AWS**: **RDS, DynamoDB, DocumentDB, Neptune e Aurora**.

## Hands On (vídeos)
**Primeiro vídeo**: os provedores de cloud e suas tecnologias, as opções do mercado e os **benefícios e riscos** de adotar um banco como serviço. **Na sequência**: as soluções de bancos da **AWS** na prática: o **console**, os recursos e ferramentas, **pricing** e o provisionamento de bases de exemplo.

## Cloud computing
- Um **modelo de entrega** de serviços de computação com **acesso sob demanda** a recursos de TI **compartilhados pela internet**. Em vez de possuir e gerenciar os próprios recursos, os usuários os **alugam** de provedores, que mantêm a infraestrutura (servidores, armazenamento, redes e software).

| Modelo | O provedor fornece | Para o usuário |
|---|---|---|
| **IaaS** (Infrastructure-as-a-Service) | Infraestrutura **virtualizada**: servidores virtuais, armazenamento, redes | **SO, aplicativos e configurações** |
| **PaaS** (Platform-as-a-Service) | Uma **plataforma de desenvolvimento** completa: infraestrutura, ambiente de execução e serviços como **bancos e filas** | O **desenvolvimento** dos aplicativos |
| **SaaS** (Software-as-a-Service) | **Aplicativos completos** pela internet, acessados pelo **navegador** | Só o uso, sem instalar ou gerenciar |

- **Vantagens**: escalabilidade flexível · acesso sob demanda · **redução de custos operacionais** · alta disponibilidade · facilidade de gerenciamento · **atualizações automáticas**.
- **Por que surgiu**: avanços tecnológicos (processamento, armazenamento, banda) · **virtualização** (ambientes isolados num único hardware) · demanda por **escalabilidade e flexibilidade** · **redução de custos** (**pay-as-you-go**) · colaboração e acesso remoto.
- **Marco inicial**: o lançamento da **AWS em 2006**, com o **Amazon S3** e o **Amazon EC2**. Depois vieram **Google Cloud Platform, Microsoft Azure e IBM Cloud** (Figura 1).

## DBaaS
- **Database-as-a-Service**: provedores de nuvem oferecem **serviços de banco de dados pagos**. Em vez de configurar, instalar e gerenciar um banco num servidor, contrata-se um banco **gerenciado e configurado** conforme a necessidade.
- Oferecem bancos **relacionais, NoSQL** e outros, geralmente com **backup e recuperação, escalabilidade automática, monitoramento e segurança**.
- **Atenção**: os usuários precisam estar cientes dos **custos** e de **possíveis limitações** impostas pelos provedores.

| Benefício | O que o PDF diz |
|---|---|
| **Implantação e gerenciamento** | O provedor cuida de servidores, rede e software; a equipe foca no uso do banco |
| **Escalabilidade automática** | **Vertical** (aumentar ou diminuir recursos) ou **horizontal** (adicionar ou remover nós), conforme a carga |
| **Alta disponibilidade e confiabilidade** | Os provedores **geralmente** implementam replicação, **backups automatizados**, monitoramento contínuo e **recuperação de desastres** |
| **Manutenção simplificada** | Patches de segurança, atualizações e otimizações pelo provedor |
| **Segurança e conformidade** | **Criptografia em repouso e em trânsito**, controle de acesso, auditorias, conformidade |
| **Redução de custos** | Paga-se só pelo que usa; economia em administração, monitoramento e backup |

## DBaaS na AWS
| Serviço | O que o PDF diz |
|---|---|
| **Amazon RDS** (Relational Database Service) | Relacional **gerenciado**: **MySQL, PostgreSQL, Oracle, SQL Server e MariaDB**, com **backups automáticos**, monitoramento e **failover** |
| **Amazon DynamoDB** | **NoSQL** totalmente gerenciado, **escalável e de baixa latência**; popular para apps móveis e web, **jogos** e **IoT** |
| **Amazon DocumentDB** | NoSQL gerenciado **compatível com MongoDB**; análise de dados, IoT e web |
| **Amazon Neptune** | Banco **de grafos** totalmente gerenciado; redes sociais, conhecimento de domínio, recomendações; análise de dados e **machine learning** |
| **Amazon Aurora** | Relacional **compatível com MySQL e PostgreSQL**; **missão crítica** e grandes cargas |

- A melhor opção **depende dos requisitos** do negócio. Ver a Figura 2 (principais recursos de DBaaS da AWS).

## Referências
Amazon DynamoDB Documentation · Amazon RDS and Aurora Documentation · Creating an Amazon RDS DB instance · Erl, Puttini e Mahmood · Garcia-Molina et al. · Petrov, *Database Internals* · Sharma e Sood · Tiwari e Srivastava · Wittig e Wittig
