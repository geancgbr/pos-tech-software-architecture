---
tags: [pos-tech/fase-1, documentacao, conceito]
aliases: [C4, Modelo C4, System Landscape, Diagrama de Contexto, Diagrama de Contêiner, Diagrama de Componente]
---

# C4 Model

Criado por **Simon Brown**. Documenta a arquitetura em **4 níveis de abstração**, do macro ao micro, para que cada público veja o nível relevante sem sobrecarga. Destaca-se pela **simplicidade e modularidade** e faz a transição gradual entre [[HLD e LLD (High-Level Design e Low-Level Design)|HLD e LLD]].

| Nível | Mostra | Para quê |
|---|---|---|
| **C1 Contexto** | Propósito do sistema, usuários e sistemas externos | Alinhar o técnico e o negócio (comparável ao HLD) |
| **C2 Contêiner** | Grandes blocos (front-end, back-end, bancos, APIs, servidores) e suas interações | Responsabilidades e dependências (intermediário entre HLD e LLD) |
| **C3 Componente** | Módulos internos de cada contêiner | Coesão e modularidade; onde implementar |
| **C4 Código** | Estrutura de classes e organização do código | **Opcional**: auditorias, manutenção |

- **System Landscape**: um "mapa" dos sistemas da organização. É um diagrama de contexto **sem foco num sistema específico**.
- Os vídeos também tratam do uso do C4 em **diagramas de Deployment**.
- No template do [[DAS (Design Approval Sheet)|DAS]], a estrutura C4 vai de C1 a C3.

Exemplos dos níveis (sistema bancário): [[DOC 03 - Modelos e diagramas de arquitetura - C4 Model#Os 4 níveis]]

Aparece em: [[DOC 01 - Introdução à documentação de arquitetura]], [[DOC 03 - Modelos e diagramas de arquitetura - C4 Model]], [[DOC 06 - DAS (Design Approval Sheet)]]
