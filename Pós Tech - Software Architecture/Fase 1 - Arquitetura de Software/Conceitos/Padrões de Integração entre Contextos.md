---
tags: [pos-tech/fase-1, ddd, conceito]
aliases: [Context Mapping Patterns, Parceria, Kernel Compartilhado, Shared Kernel, Cliente-Fornecedor, Customer-Supplier, Conformista, Conformist, Camada Anticorrupção, ACL, Anti-Corruption Layer, Serviço de Host Aberto, OHS, Open-Host Service, Linguagem Publicada, Published Language, Caminhos Separados, Separate Ways, Grande Bola de Lama, Big Ball of Mud]
---

# Padrões de Integração entre Contextos

Como dois [[Contexto Delimitado|contextos]] (e seus times) se integram. **U** = upstream (fornecedor) · **D** = downstream (cliente).

## Cooperação: os times colaboram, sem precedência
- **Parceria**: comunicação constante. Cada time avisa o outro das mudanças e dá tempo e documentação para ele se adaptar. É comum no começo do desenvolvimento.
- **Kernel compartilhado**: uma parte do modelo e do código é comum aos contextos. Qualquer mudança afeta todos e precisa ser testada em todos. **Desencorajado** porque fere a ideia de limites, mas é inevitável em **legado/monólito** durante a modernização.

## Cliente-fornecedor: dependência por serviço
- **Conformista**: U não negocia, e D **se conforma** com o modelo que recebe. Exemplo: provedor externo de OAuth 2.0 que atende clientes no mundo todo.
- **Camada anticorrupção (ACL)**: nem U nem D cedem, então D cria uma camada que **traduz** o modelo de U para o seu e preserva sua integridade. Use quando:
  1. D tem um subdomínio **principal** a proteger;
  2. o modelo de U é ineficiente ou não serve totalmente (comum com legado);
  3. U muda de protocolo com frequência, e assim a manutenção fica só na ACL.
- **Serviço de host aberto (OHS)**: D tem a preferência. U expõe um **protocolo aberto e estável**, separado da implementação interna.
- **Linguagem publicada**: OHS mais uma abstração na linguagem de cada cliente, que pode ter versões personalizadas. Exemplos: adquirentes e cartões, EDI na logística, manufatura.

## Sem integração
- **Caminhos separados**: integrar custa mais que duplicar, ou os times nem conseguem se comunicar. Cada um faz o seu. Exemplos: relatórios, autenticação, logs.
- **Grande bola de lama** (Vernon): sistema grande sem limites claros. Cerque-o com uma linha, **não aplique modelagem sofisticada** e **impeça que contamine** os outros contextos.

> [!tip] Resumo: Conformista, ACL e OHS
> - **Conformista**: D aceita o modelo de U.
> - **ACL**: D traduz o modelo de U.
> - **OHS**: U facilita a vida de D com um protocolo estável.

Tudo isso aparece desenhado no [[Mapa de Contexto]].

Aparece em: [[DDD 04 - Trabalhando com contextos delimitados]]
