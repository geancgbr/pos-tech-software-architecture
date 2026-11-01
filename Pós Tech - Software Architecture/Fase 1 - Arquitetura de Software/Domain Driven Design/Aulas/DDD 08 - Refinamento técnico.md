---
tags: [pos-tech/fase-1, ddd, aula]
disciplina: Domain Driven Design
aula: 8
fonte: "Aula 08- Refinamento técnico.pdf"
---

# DDD 08 - Refinamento técnico

← [[DDD 07 - Levantamento de requisitos]] · [[Domain Driven Design]] · Próxima → [[DDD 09 - Definition of Ready e Definition of Done]]

> [!summary] Em uma frase
> O [[Refinamento Técnico]] transforma o requisito de negócio numa especificação técnica viável: dúvidas por etapa da jornada, validação com [[Spike e POC]], desenho de arquitetura, requisito técnico e [[Estimativas (Planning Poker e Monte Carlo)|estimativa]].

## Etapas
1. **Refinar a jornada do usuário**: percorra cada etapa da jornada da solução anotando **dúvidas e considerações técnicas**. Isso dá à referência técnica a base para pensar nas opções.
2. **Validar com [[Spike e POC|Spikes e POCs]]**:
   - **Spike**: item **dentro da sprint** para explorar uma solução e ganhar conhecimento, em fluxos ou validações complexas.
   - **POC** (prova de conceito): valida se uma solução técnica atende ao objetivo **antes de ir para produção**.
   - Os dois reduzem o risco técnico e deixam as estimativas mais realistas.
3. **Desenhar a arquitetura** (exemplo do CRM):
   - Front-end: React ou Vue, falando com o back por REST ou GraphQL.
   - Back-end: Node.js, Python ou .NET Core, com a lógica de negócio.
   - Banco: relacional (PostgreSQL, MySQL) ou NoSQL (MongoDB).
   - Autenticação: Auth0 ou OAuth2.
   - **API Gateway**: ponto único de entrada (autenticação, autorização, monitoramento de tráfego).
   - **Microsserviços em cloud** (AWS, GCP, Azure), para escalar cada parte separadamente.
   - **Filas e mensageria** (RabbitMQ, Kafka), para processamento assíncrono sem travar o front.
   - **Monitoramento e log** (ELK, Prometheus e Grafana).
   - **Segurança** em todas as camadas (criptografia em repouso e em trânsito, firewall, desenvolvimento seguro).
4. **Preencher o requisito técnico da solução** (checklist abaixo).
5. **Estimar**: veja [[Estimativas (Planning Poker e Monte Carlo)]].

## Checklist do requisito técnico
- [ ] Descrição detalhada da solução
- [ ] Tecnologias e ferramentas, **com a justificativa** de cada uma
- [ ] Integrações e dependências (APIs, terceiros, bases)
- [ ] Estratégia de implementação (ágil, CI/CD, code review)
- [ ] Segurança e conformidade
- [ ] Escalabilidade e manutenibilidade
- [ ] Testes (unitários, integração, desempenho, segurança)
- [ ] Documentação (técnica, manual do usuário, operação)
- [ ] Plano de implantação (ambientes, rollout e **rollback**)
- [ ] Critérios de aceitação e validação
