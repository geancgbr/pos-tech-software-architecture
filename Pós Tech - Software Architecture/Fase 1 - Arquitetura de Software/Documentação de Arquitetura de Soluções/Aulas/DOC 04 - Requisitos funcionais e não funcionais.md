---
tags: [pos-tech/fase-1, documentacao, aula]
disciplina: Documentação de Arquitetura de Soluções
aula: 4
fonte: "11SOAT - Fase 3 - Documentação de arquitetura de soluções - Aula 4.pdf"
---

# DOC 04 - Requisitos funcionais e não funcionais

← [[DOC 03 - Modelos e diagramas de arquitetura - C4 Model]] · [[Documentação de Arquitetura de Soluções]] · Próxima → [[DOC 05 - Architecture Decision Records (ADRs)]]

> [!summary] Em uma frase
> Os [[Requisitos Funcionais e Não Funcionais|requisitos funcionais]] definem **o que** o sistema deve fazer, e os **não funcionais** definem **como** ele deve se comportar (qualidade). Hoje eles são construídos de forma **colaborativa**, com o [[Arquiteto de Soluções|arquiteto de soluções]] fazendo o elo entre o negócio e a técnica.

## Hands On (vídeos)
Explicações visuais e práticas sobre o papel de cada tipo de requisito, exemplos em vários cenários e boas práticas de documentação.

## Por que documentar
Os requisitos definem as expectativas e necessidades do sistema para usuários e negócio. Documentá-los alinha as metas entre desenvolvimento e negócio, reduz ambiguidades, previne retrabalho e permite aos stakeholders verificar se a solução atende aos objetivos.

## Funcionais × não funcionais
| | Requisitos funcionais | Requisitos não funcionais |
|---|---|---|
| Definem | **O que** o sistema deve fazer: ações, operações, comportamentos | **Como** o sistema deve se comportar: qualidades |
| Aspectos | Interações dos usuários; objetivos de negócio | Desempenho, usabilidade, segurança, escalabilidade, confiabilidade |
| Regra | Cada um deve ser **específico** e **testado** | Garantem a qualidade e a satisfação do usuário |
| Sem eles | Funcionalidades faltando ou interpretadas errado | Problemas de desempenho, segurança e escalabilidade |
| Exemplos | "Permitir que o usuário faça login e acesse seu perfil" · "Processar pedidos de compra" · "Gerar relatórios de vendas" · Banco: "transferir fundos entre contas" · E-commerce: "adicionar ao carrinho e fazer checkout" · Rede social: "publicar fotos e ver comentários" | "Responder em até **2 segundos**" · "Suportar até **10.000 usuários simultâneos**" · E-commerce: resposta abaixo de 2 s para não frustrar o cliente · Saúde: "dados dos pacientes **criptografados em todas as transferências**" |

## Levantamento de requisitos
- Identifica as necessidades da empresa no desenvolvimento ou na manutenção de um produto, **com os stakeholders**.
- **Primeiro passo**: envolver os stakeholders em **reuniões**, para um entendimento profundo, informações completas e expectativas alinhadas. É preciso ajudá-los a entender o ambiente em que atuam e como criar a solução em equipe. O guia está na Figura 1 do PDF.

| | Modelo tradicional | Hoje |
|---|---|---|
| Quando | **Todos** os requisitos definidos no início ("coletar" requisitos) | Contínuo: é impossível prever tudo no início |
| Quem | O(a) analista de sistemas definia tudo | **Colaborativo** |
| Característica | Burocrático e pouco adaptável | Feedback contínuo; a arquitetura define estrutura e padrões que facilitam integrar novos requisitos |

## Os papéis na construção dos requisitos
- **Product Manager (PM)**: define a **visão do produto**.
- **Product Owner (PO)**: traduz a visão em **histórias de usuário** e trabalha com o time.
- **Time técnico**: testa, refina e dá **feedback constante**.
- **Arquitetura**: garante a **coerência técnica** e o alinhamento de longo prazo.
- **[[Arquiteto de Soluções]]**: **coordena** essas interações. É o elo entre o negócio e a implementação: entende as necessidades com os stakeholders, define a estrutura e os componentes, toma as decisões técnicas estratégicas, escolhe tecnologias, estabelece padrões e antecipa e mitiga riscos com sua visão holística.

O mapa de requisitos está na Figura 2 do PDF.

## Problemas comuns e boas práticas
**Problemas**: falta de clareza ou de documentação completa · falta de comunicação entre equipes (interpretações divergentes, erros, retrabalho).

**Boas práticas**:
- lista clara e detalhada de requisitos;
- linguagem objetiva;
- **validar cada requisito com os stakeholders**;
- **organizar por prioridade**;
- manter a documentação **atualizada**;
- **templates e frameworks padronizados**, principalmente em projetos grandes.

A documentação dos requisitos também é uma **referência ao longo do ciclo de vida**: as mudanças são feitas de forma controlada e o sistema continua alinhado ao negócio.

## Mercado, cases e tendências
Leitura recomendada: *Engenharia de Requisitos: Software Orientado ao Negócio* (2016), de Carlos Eduardo Vazquez e Guilherme Siqueira Simões.

## Referências
Vazquez e Simões, *Engenharia de requisitos* · Richards e Ford, *Fundamentos da Arquitetura de Software* (2020) · Rosa, *Requisitos de software funcionais e não funcionais* (SoftDesign, 2021) · Souza, *Requisitos Não Funcionais* (DevMedia, 2010)
