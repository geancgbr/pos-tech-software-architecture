---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [mTLS, TLS, Mutual TLS, Criptografia, Client Authentication, Dados em repouso, Dados em trânsito]
---

# Criptografia e mTLS

## Segurança de dados e criptografia
Proteger os dados **armazenados e transmitidos** ([[MS2 05 - Realizando o deploy de microsserviços]]).
- **Em repouso**: algoritmos robustos (**AES-128/192/256, RSA**) contra força bruta.
- **Em trânsito**: **TLS** associado às chamadas HTTP, ou até TCP, mantendo o protocolo atualizado.
- **Chaves**: soluções robustas, por exemplo um **cofre de senhas**, sem compartilhar as chaves, com auditoria. **Rotação** regular.
- **Segurança em camadas**: ex.: **WAF**.
- **GDPR e LGPD**: dados **pessoais** (CPF, RG, e-mail, nome) e **pessoais sensíveis** (gênero, altura, doença).

## mTLS
Autenticação **bidirecional** com **certificados digitais** (recurso **Client Authentication** do TLS): criptografa e verifica a identidade **das duas partes**.
- Gerar chaves e certificados assinados por uma **CA** → configurar cliente e servidor para **exigir certificados** → validar no **handshake TLS**.
- Boas práticas: **rotação** (ex.: certificados de 1 ano) · **CA confiável** (pública, como a DigiCert, ou privada) · **monitoramento** das falhas.

## Na disciplina Resiliência em Microsserviços (Fase 4)
No [[Service Mesh]], os **proxies sidecar** implementam **mTLS** e o **Control Plane** emite e distribui os certificados ([[RES 04 - Service Mesh e controle de tráfego]]).

## Na disciplina Privacidade de Dados e LGPD (Fase 5)
- Transformar informações legíveis em **texto cifrado**; a **assimétrica** é apresentada como o modo mais seguro, mas também **uma das mais frágeis** (perder ou vazar a chave) ([[LGPD 02 - A segurança dos usuários e de seus dados]]).
- **At-rest** (o tipo mais conhecido; problemas: gerenciar e perder chaves, consumo de processamento) e **in-transit** (ex.: **HTTPS**; confiar na infraestrutura **pode ser considerado** um **risco calculado**) ([[LGPD 06 - LGPD no desenvolvimento de software]]).
- Na revisão: proteção no armazenamento e na transferência; "um modo seguro" de armazenar e transportar ([[LGPD 07 - Considerações finais na LGPD]]).

Aparece em: [[MS2 05 - Realizando o deploy de microsserviços]], [[RES 04 - Service Mesh e controle de tráfego]], [[LGPD 02 - A segurança dos usuários e de seus dados]], [[LGPD 06 - LGPD no desenvolvimento de software]], [[LGPD 07 - Considerações finais na LGPD]]
