---
tags: [pos-tech/fase-4, banco-de-dados, cloud, conceito]
aliases: [DBaaS, Database-as-a-Service, Cloud computing, Computação em nuvem, IaaS, PaaS, SaaS]
---

# DBaaS (Database-as-a-Service)

## Cloud computing
Acesso **sob demanda** a recursos de TI **compartilhados pela internet**, alugados de provedores ([[DE 06 - Cloud e DBaaS]]).
- **IaaS**: infraestrutura virtualizada; o usuário controla SO, aplicativos e configurações. **PaaS**: plataforma de desenvolvimento completa (incluindo bancos e filas). **SaaS**: aplicativos completos pelo navegador.
- **Vantagens**: escalabilidade, acesso sob demanda, menos custo operacional, alta disponibilidade, gerenciamento fácil, atualizações automáticas.
- **Marco inicial**: a **AWS em 2006** (S3 e EC2); depois GCP, Azure e IBM Cloud.

## DBaaS
O provedor de nuvem entrega um **banco de dados gerenciado e configurado**, pago, em vez de o usuário instalar e gerenciar o próprio.
- **Benefícios**: implantação e gerenciamento fáceis · **escalabilidade automática** (vertical e horizontal) · alta disponibilidade (replicação, backups, recuperação de desastres) · manutenção pelo provedor · segurança (criptografia em repouso e em trânsito) · redução de custos.
- **Atenção**: **custos** e **possíveis limitações** do provedor.
- **Na AWS**: **RDS** (MySQL, PostgreSQL, Oracle, SQL Server, MariaDB) · **DynamoDB** · **DocumentDB** (compatível com MongoDB) · **Neptune** (grafos) · **Aurora** (MySQL e PostgreSQL, missão crítica).
- **Outros DBaaS citados**: MongoDB **Atlas** ([[MongoDB]]) e Neo4j **Aura** ([[Neo4j]]).

## Na disciplina Privacidade de Dados e LGPD (Fase 5)
Um **MongoDB como serviço** aparece como exemplo de **PaaS**: o fornecedor assume grande parte das preocupações, mas os dados ficam terceirizados e o operador continua responsável ([[IaaS, PaaS e SaaS]]) ([[LGPD 05 - LGPD na implementação da solução de tecnologia]]).

Aparece em: [[DE 02 - Bancos de documentos com MongoDB]], [[DE 05 - Bancos orientados a grafos com Neo4j]], [[DE 06 - Cloud e DBaaS]], [[LGPD 05 - LGPD na implementação da solução de tecnologia]]
