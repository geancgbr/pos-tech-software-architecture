---
tags: [pos-tech/fase-1, ddd, conceito, design-tatico]
aliases: [Aggregate, Agregados]
---

# Agregado

Conjunto de [[Entidade|entidades]] e [[Objeto de Valor|objetos de valor]] relacionados, com um **limite** que o define.

- **Consistência forçada**: **só a lógica do próprio agregado altera seu estado**, o que garante a integridade e as regras de negócio.
- Objetos de fora **podem ler**, mas **não alterar**. Eles **pedem** a mudança por meio de **comandos** expostos em interfaces do agregado.
- No [[Event Storming]], os agregados surgem ao agrupar comandos e eventos pelo **objeto principal** (por exemplo, o agregado de Notas).

## Na disciplina Estrutura de Microsserviços Parte II (Fase 4)
- **Aggregates**: grupos de **entidades e objetos de valor** tratados como **uma unidade**; um Aggregate pode ficar **dentro de um único serviço**, ajudando na consistência e nas operações transacionais.
- No Hands On, o padrão **pode auxiliar** a lidar com a **concorrência**; segundo o resumo, toda alteração em entidades e value objects é **versionada a partir da entidade principal** ([[MS2 02 - Aplicando a lógica de negócios no microsserviço]]).

Aparece em: [[DDD 05 - Implementando arquitetura e lógica]], [[DDD 06 - Event Storming]], [[MS2 02 - Aplicando a lógica de negócios no microsserviço]]
