---
tags: [pos-tech/fase-1, arquitetura, conceito]
aliases: [Atores condutores, Atores conduzidos, Driving actors, Driven actors, Repository, Recipient]
---

# Atores Condutores e Conduzidos

**Atores** são as coisas do mundo real com que a aplicação interage, **fora do hexágono**: seres humanos, outros aplicativos, dispositivos de hardware ou software.

| | Condutores | Conduzidos |
|---|---|---|
| Lado | **Esquerdo** | **Inferior direito** |
| Recebem chamadas | **De fora** do sistema, e as encaminham às **portas de entrada** | **De dentro** (dos casos de uso), e as direcionam a sistemas externos |
| Quem aciona quem | O ator **conduz** a interação com o centro | O **centro aciona** o ator, por meio das **portas secundárias** |
| Exemplos | Requisição HTTP, suíte de testes, API (RESTful, GraphQL), app mobile, terminal/CMD, páginas web | Banco de dados, SMTP, sistema de arquivos, chamadas HTTP, serviços de terceiros |

O lado direito tem os **serviços intercambiáveis e flexíveis** que dão à solução a infraestrutura de que ela precisa para existir.

## Tipos de ator conduzido
- **Repositório (Repository)**: **envia e recebe** informações. Exemplo: banco de dados ou outro armazenamento.
- **Destinatário (Recipient)**: só **envia e esquece**. Exemplo: envio de e-mail por SMTP.

No Hands On, foram criados atores conduzidos para **cache** e para **persistência da entidade Usuários**.

Aparece em: [[ARQ 05 - Arquitetura Hexagonal]]
