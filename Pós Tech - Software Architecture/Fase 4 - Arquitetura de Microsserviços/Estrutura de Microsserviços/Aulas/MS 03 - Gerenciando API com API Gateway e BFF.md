---
tags: [pos-tech/fase-4, microsservicos, api-gateway, aula]
disciplina: Estrutura de Microsserviços
aula: 3
fonte: "Estrutura de Microsserviços/Estrutura de Microsserviços - Aula 3.pdf"
---

# MS 03 - Gerenciando API com API Gateway e BFF

← [[MS 02 - Comunicação entre processos com microsserviços]] · [[Estrutura de Microsserviços]] · Próxima → [[MS 04 - Modelo de API para microsserviços]]

> [!summary] Em uma frase
> O **[[API Gateway]]** desacopla os clientes dos serviços e pode implementar **Service Discovery**, **Circuit Breaker** e **[[API Composition]]**, além de **segurança**, **rate limit** (com **backpressure** e HTTP **429**), **cache** e métricas. As soluções de mercado trazem uma plataforma de **API Management**. O **[[Backend for Frontend (BFF)|BFF]]** cria **um backend por interface de usuário**; no BFF, cada cliente tem seu **API Gateway dedicado**.

## Hands On
Criar o **API Gateway dedicado ao App FIAP Store**, no padrão **BFF**, expondo o serviço **Estoque** pelo **[[Kong]]**:
- Baixar o repositório da aula 3 e instalar o **Primate**, para configurar o Kong **graficamente**.
- Montar o Kong com **duas réplicas** do Estoque usando **Docker Compose**.
- Configurar o **self-register** no Estoque, para que cada nova instância se registre no **upstream `estoque`** do Kong (adaptando o `main.py`).
- Configurar uma política de autenticação **Basic Auth**.

## API Gateway
- **Desacopla** os clientes dos serviços: mudanças nos serviços são configuradas no gateway **sem impactar os clientes**, respeitando o **contrato** da API.
- Por intermediar tudo, pode implementar **Service Discovery** e **Circuit Breaker**. Dependendo da solução, também **API Composition**: várias chamadas agregadas numa resposta.
  - **Exemplo**: a tela de produto do App precisa de descrição, preço e estoque. Um endpoint no gateway chama **Catálogo de Produtos**, **Estoque** e **Precificação** e agrega tudo **num único JSON** (Figura 1).
- **Segurança**: validação de credenciais e controle de acesso a endpoints conforme o perfil.
- **Rate limit**: uma taxa de requisições por intervalo (segundo, minuto, hora). Ao ultrapassar, aplica **backpressure**: interrompe as novas e devolve **HTTP 429 Too Many Requests**, protegendo o serviço.
- **Cache**: guarda por um tempo as respostas das operações mais usadas.
- **Métricas e logs** (normalmente armazenados pelo gateway): análise, alertas e até **monetização** (relatórios de uso por cliente) e **log de auditoria**.

| Vantagens | Desvantagens |
|---|---|
| Abstrai toda a estrutura da aplicação (monolito ou microsserviços) | **Mais um componente** para implantar e sustentar |
| Acrescenta capacidades por **políticas** (Service Discovery, Circuit Breaker, API Composition...), só com configuração | **Ponto central**: se cair, interrompe toda a comunicação; prever **alta disponibilidade** |
| — | Toda alteração nos serviços precisa ser **refletida no gateway** |

## API Management
Normalmente um site web ou app desktop das soluções de mercado, para: configurar os módulos de API no gateway (políticas, rotas, serviços) · gerir as **aplicações clientes** (credenciais, controle de acesso) · **relatórios de uso** · métricas e logs · **contratos** publicados.

## BFF (Backend for Frontend)
- Arquitetura **cada vez mais usada** com microsserviços: **um backend específico para cada interface de usuário (UI)**, otimizando a comunicação entre o frontend e os microsserviços.
- **Intermediário** que **agrega e formata** os dados de vários serviços, entregando **só o necessário** (melhor performance).
- **Continuidade da API**: uma squad cuida do **seu API Gateway dedicado**, sem impactar outras.
- **Escalabilidade** dedicada ao cliente específico, com **custos mais previsíveis**; instância **mais leve** (só o módulo do cliente alvo); métricas e logs **já segmentados** (Figura 2).

## Referências
Kong Docs: Kong Gateway · Kong Plugin Hub · Richardson, *Microservices Patterns* · Richardson: API Composition · API Gateway / Backends for Frontends
