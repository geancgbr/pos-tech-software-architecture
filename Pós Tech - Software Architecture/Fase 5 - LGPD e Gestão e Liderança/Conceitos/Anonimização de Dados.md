---
tags: [pos-tech/fase-5, lgpd, conceito]
aliases: [Anonimização, Dados anonimizados, Mascaramento de dados, Mascaramento dinâmico, Faker]
---

# Anonimização de Dados

Transformar dados pessoais para **impossibilitar a identificação direta ou indireta** de um indivíduo, de forma **irreversível**, mesmo combinando com outras informações ([[LGPD 02 - A segurança dos usuários e de seus dados]]).

> [!note] Na aula 2, impede a identificação "direta ou indireta"; na aula 7, "diretamente".

- A LGPD considera os dados anonimizados **fora da definição de dados pessoais** ([[LGPD 02 - A segurança dos usuários e de seus dados]]) e **fora do escopo** da lei ([[LGPD 07 - Considerações finais na LGPD]]).
- Não é **garantia absoluta**: técnicas avançadas **podem** permitir reidentificação ([[LGPD 02 - A segurança dos usuários e de seus dados]]).
- **Processos** (exemplos): **desfiguração**, **desconexão** (dividir em unidades de armazenamento, ex.: tabelas, quebrando a relação) e **sumarização** ([[LGPD 02 - A segurança dos usuários e de seus dados]]).
- **Exemplo**: "mulher negra de 30 anos, moradora de Belo Horizonte" descreve um grupo sem particularizar ninguém; usados em **propagandas direcionadas**, mas **podem** servir à manipulação ou a crimes ([[LGPD 07 - Considerações finais na LGPD]]).
- **Em ambientes de desenvolvimento** ([[LGPD 06 - LGPD no desenvolvimento de software]]): anonimização ou **mascaramento** no transporte entre ambientes; bases com dados **falsos** (biblioteca **faker** do Python); **mascaramento dinâmico** (o menos indicado, às vezes o único viável).
- Na IA: dados **anonimizados ou consolidados** permitem treinar sem identificar diretamente os titulares ([[LGPD 07 - Considerações finais na LGPD]]). Na equipe técnica: considerar a anonimização sempre que possível (art. 46º) ([[LGPD 01 - Introdução à LGPD e seus princípios básicos]]).

> [!warning] A aula 7 diz que os anonimizados ficam fora do escopo e, em seguida, que "alguns dos dados anonimizados são considerados sensíveis" (art. 5, II).

Aparece em: [[LGPD 01 - Introdução à LGPD e seus princípios básicos]], [[LGPD 02 - A segurança dos usuários e de seus dados]], [[LGPD 06 - LGPD no desenvolvimento de software]], [[LGPD 07 - Considerações finais na LGPD]]
