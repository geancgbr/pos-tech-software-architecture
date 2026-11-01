---
tags: [pos-tech/fase-4, microsservicos, seguranca, aula]
disciplina: Estrutura de Microsserviços Parte II
aula: 5
fonte: "Estrutura de Microsserviços Parte II/Estrutura de Microsserviços II - Aula 5.pdf"
---

# MS2 05 - Realizando o deploy de microsserviços

← [[MS2 04 - Testando microsserviços, parte 2]] · [[Estrutura de Microsserviços Parte II]] · Próxima → [[MS2 06 - Realizando o deploy de microsserviços, parte 2]]

> [!summary] Em uma frase
> **Segurança no acesso aos serviços**, **configuração externalizada**, os padrões **chassis** e **service mesh** e os tipos de deployment. O texto do PDF trata da **segurança de dados e criptografia** (em repouso e em trânsito), do **mTLS** e das **estratégias de deployment**: **Recreate, Blue-Green, Canary, Rolling Update, Teste A/B e Shadow**. Ver [[Criptografia e mTLS]] e [[Estratégias de Deployment]].

## Hands On (vídeo)
Nas **videoaulas**: criar um **cluster mínimo de Kubernetes** com a **service mesh Istio**, publicar serviços nela, validar e configurar **policies**. Repositório da aula 5 e **Postman**.

**Segundo o resumo**:
- **Tokens de acesso OAuth 2.0** para autenticar as aplicações clientes, com desacoplamento.
- **Variáveis de ambiente e arquivos de configuração** injetados em cada ambiente (configuração externalizada).
- **Chassis e service mesh** possibilitam implementar **descoberta de serviços, circuit breaker e observabilidade**, entre outras funcionalidades,, por **bibliotecas/frameworks** ou por **proxies** que intermediam o tráfego.
- Tipos de deployment: **tradicional, VM, containers e serverless**.

## Segurança de dados e criptografia
- Proteger os dados **armazenados e transmitidos** contra acesso e modificação não autorizados. A **criptografia** protege **integridade e confidencialidade**: só quem tem a **chave** consegue ler.
- **Armazenamento seguro**: algoritmos robustos como **AES-128, AES-192, AES-256 e RSA**, importantes para evitar que ataques de **força bruta** sejam bem-sucedidos.
- **Transmissão segura**: **TLS** nas chamadas HTTP, ou até TCP, acompanhando as atualizações do protocolo.
- **Gerenciamento de chaves**: soluções robustas, **por exemplo** de **cofre de senhas**, que montam as chaves nos serviços **sem compartilhá-las**, com poucas pessoas com acesso e **registro para auditoria**.
- **Melhores práticas**: **rotação de chaves** · **auditoria e monitoramento** (alertas para atividades suspeitas) · **segurança em camadas** (ex.: **WAF**, Web Application Firewall).
- **Normas**: **GDPR** e **LGPD** classificam os tipos de dados, como **pessoais** (identificação: CPF, RG, e-mail, nome) e **pessoais sensíveis** (passíveis de discriminação: gênero, altura, doença). Garantir a criptografia **em repouso** (disco ou RAM) e **em trânsito** (HTTPS) evita vazamentos e prejuízos **financeiros e reputacionais**.

## mTLS
- Autenticação **bidirecional** com **certificados digitais**: criptografa os dados e verifica a **identidade das duas partes**. É um recurso do TLS chamado **Client Authentication**.
- Útil em microsserviços, onde muitos serviços se comunicam.
- **Como usar**: (1) **gerar** par de chaves e certificados assinados por uma **Autoridade Certificadora (CA)** para cliente e servidor; (2) **configurar** os dois para **exigir certificados**; (3) no **handshake TLS**, os dois apresentam e validam os certificados.
- **Melhores práticas**: **rotação de certificados** (ex.: duração de **1 ano**) · **validação rigorosa** da CA (pública confiável, como a **DigiCert**, ou **privada** sob gestão de um time) · **monitoramento e alertas** de falhas.

## Estratégias de deployment
Cada uma tem vantagens, desvantagens e casos de uso; escolher a mais indicada para cada serviço (Figuras 1 a 6, Container Solutions).

| Estratégia | O que é | Por que é importante | Como usar |
|---|---|---|---|
| **Recreate** | Remove **todas** as instâncias antigas antes de implantar as novas | Todas na nova versão: consistência, para apps que **não suportam versões simultâneas** | Parar tudo e lançar a nova; ideal quando se **tolera inatividade** |
| **Blue-Green** | Duas versões **em paralelo**: **Blue** (atual) e **Green** (nova) | Testar a nova num ambiente idêntico e **reverter rápido** | Dois ambientes idênticos e alternar o tráfego por **balanceador** |
| **Canary Release** | Liberação **gradual** para um **subconjunto** de usuários (uma porcentagem, sem distinção de quais) | Testar com **usuários reais** em produção antes do lançamento completo | Direcionar um **percentual do tráfego** e monitorar |
| **Rolling Update** | Atualiza as instâncias **gradualmente**, uma a uma ou em lotes | Minimiza inatividade e facilita a reversão | Ferramentas de atualização progressiva, como o **Kubernetes** |
| **Teste A/B** | Divide o tráfego entre **duas versões** para **comparar** | Avaliar funcionalidades por métricas (engajamento, conversão); permite **Beta Users** | Versão A (atual) e B (nova); dividir por aleatoriedade, segmentação (beta, alpha users), geolocalização; analisar os dados |
| **Shadow Deployment** | Roda a nova versão em paralelo, **sem expô-la** aos usuários | Testar **em produção** sem afetar os usuários | **Duplicar o tráfego real** com balanceador ou proxy reverso (**NGINX, HAProxy**, service mesh como **Istio**) |

> [!note] O "O que vem por aí" fala de segurança no acesso aos serviços, configurações externalizadas, chassis, service mesh e tipos de deployment; o resumo detalha OAuth 2.0 e os tipos tradicional, VM, containers e serverless; o Saiba Mais do PDF trata de criptografia, mTLS e estratégias de deployment.

## Referências
Container Solutions: Kubernetes deployment strategies · Richardson, *Microservices Patterns* · Richardson: Access token · Externalized configuration · Microservice chassis · Serverless deployment · Service instance per container · Service Instance per VM · Service mesh · Single Service Instance per Host
