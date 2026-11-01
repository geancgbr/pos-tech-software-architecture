---
tags: [pos-tech/fase-4, microsservicos, conceito]
aliases: [Service Discovery, Service Registry, Self registration, Self-register]
---

# Descoberta de Serviços

Como os serviços são **dinâmicos** (vários servidores, escala horizontal), é preciso descobri-los de forma confiável ([[MS 02 - Comunicação entre processos com microsserviços]]).

- **Self registration**: o serviço se registra ao iniciar (geralmente nome e localização, como IP e porta; possivelmente versão ou health check).
- **Service Registry**: consultado, geralmente, pelo **nome** do serviço; mantém a lista por **health checks** regulares ou por **heartbeat** (os serviços avisam quando estão saindo).
- **Client-side**: o cliente consulta o registry e balanceia. **Server-side**: um **roteador intermediário** consulta, roteia e pode balancear.
- **Ferramentas**: Consul, Etcd, Eureka (Netflix), Apache Zookeeper.
- **Na aula 3**: cada instância do Estoque se registra no **upstream `estoque`** do **Kong**; o API Gateway pode implementar o padrão ([[MS 03 - Gerenciando API com API Gateway e BFF]]).

## Na disciplina Resiliência em Microsserviços (Fase 4)
No [[Service Mesh]], o **Control Plane** mantém o registro dos serviços e instâncias para os proxies saberem para onde rotear; o **Consul Connect** se integra nativamente ao Consul para a descoberta ([[RES 04 - Service Mesh e controle de tráfego]]).

Aparece em: [[MS 02 - Comunicação entre processos com microsserviços]], [[MS 03 - Gerenciando API com API Gateway e BFF]], [[RES 04 - Service Mesh e controle de tráfego]]
