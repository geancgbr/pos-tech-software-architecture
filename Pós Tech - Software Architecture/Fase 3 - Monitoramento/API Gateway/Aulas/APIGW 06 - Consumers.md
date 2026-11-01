---
tags: [pos-tech/fase-3, api-gateway, kong, aula]
disciplina: API Gateway
aula: 6
fonte: "API Gateway/POSTECH - Aula6_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# APIGW 06 - Consumers

← [[APIGW 05 - Criando serviços e rotas]] · [[API Gateway]]

> [!summary] Em uma frase
> Outros serviços do **[[Kong]]**: o **Konnect** (plataforma de **gerenciamento do ciclo de vida de API**, entregue como serviço), com **Dev Portal**, **Gateway Manager** e **Mesh Manager**, e as funcionalidades exclusivas do **Kong Gateway Enterprise**, como **GraphQL**, **LDAP** e **RBAC**.

## Hands On
Criar um **consumer** e usá-lo para **proteger as APIs** com plugins de **autenticação básica** e **API Key**.

> [!note] O título do PDF é "Consumers", mas o texto (Saiba Mais) trata do Konnect e da versão Enterprise. O consumer e os plugins de autenticação aparecem só no Hands On.

## Kong Konnect
| Serviço | O que o PDF diz |
|---|---|
| **Konnect** | Plataforma de **gerenciamento do ciclo de vida de API**, projetada para a **era nativa da nuvem** e **entregue como serviço**. O **plano de controle** é hospedado na nuvem pelo Kong; o **plano de dados** é gerenciado por você no seu ambiente de rede. Tudo alimentado pelo **Kong Gateway**, "leve, rápido e flexível" (Figura 2) |
| **Konnect Dev Portal** | Site **personalizável** para devs **localizarem, acessarem e consumirem** APIs: navegar e pesquisar documentação, **testar endpoints** e **gerenciar as próprias credenciais** (Figura 1). O texto acrescenta que o **Konnect** oferece opções de implantação flexíveis para APIs **internas e externas** |
| **Gateway Manager** | Módulo do Konnect para **catalogar, conectar e monitorar** o status de todos os **planos de controle** e **nós do plano de dados** num só lugar, e gerenciar a configuração do plano de controle. A visão geral lista os planos de controle da organização (Figura 3) |
| **Mesh Manager** | Criar, gerenciar e visualizar as **malhas de serviço Kong Mesh** pelo Konnect (Figura 4) |

- **Plano de controle global** (no Mesh Manager): componente central que **armazena e distribui** configurações e políticas das malhas para as **zonas locais**, **valida e aceita** conexões dos planos de controle das zonas e é **alvo das operações CLI** no mesh deployment.

## Kong Gateway Enterprise × Open Source
- O **Enterprise** tem funcionalidades que o **Open Source** não suporta:
  - **GraphQL**: converter **queries GraphQL em requests REST**, além da conversão **JQ**, e em ambos os casos definir **Rate Limit** (por exemplo, limitar as queries GraphQL).
  - Outros meios de **autenticação**, como **LDAP** e **RBAC**.
- Ver a Figura 5 do PDF (diferenças entre as versões).
- "Como aprendemos anteriormente" (diz o PDF, embora isso não esteja no texto das aulas 4 e 5), a **Open Source** atende muito bem **a maioria dos cenários**; para personalizar algo ou usar serviços exclusivos, **pode ser necessário um upgrade**.

## Referências
Kong Docs: About Gateway Manager · Dev Portal Overview · Kong Konnect
