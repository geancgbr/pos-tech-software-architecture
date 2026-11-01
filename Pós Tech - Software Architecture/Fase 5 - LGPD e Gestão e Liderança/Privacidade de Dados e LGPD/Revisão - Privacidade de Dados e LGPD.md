---
tags: [pos-tech/fase-5, lgpd, revisao]
disciplina: Privacidade de Dados e LGPD
---

# Revisão - Privacidade de Dados e LGPD

[[Privacidade de Dados e LGPD]]

> [!info] Como usar
> Tente responder antes de abrir. Clique na pergunta para ver a resposta. Errou? Anote em **Pontos fracos** no fim da nota.

## Aula 1 - Introdução
> [!question]- Qual o objetivo da LGPD, e a quem ela se aplica?
> Proteger os direitos fundamentais de liberdade e privacidade no tratamento de dados pessoais. Vale para todas as empresas e organizações que tratam dados pessoais no Brasil, de qualquer tamanho ou setor. → [[LGPD]]

> [!question]- Como deve ser o consentimento, segundo a aula 1?
> Explícito, livre, informado e inequívoco.

> [!question]- Controlador × operador?
> Controlador: decide quais dados coletar, como usar e com que propósito (usualmente o cliente que encomendou o software). Operador: lida com os dados seguindo as diretrizes do controlador (geralmente os times de desenvolvimento, projeto e operações). → [[Agentes de Tratamento]]

> [!question]- Quais os direitos dos titulares?
> Acesso, retificação, anonimização/bloqueio/eliminação, oposição, portabilidade e não ser submetido a decisões automatizadas. → [[Direitos dos Titulares]]

> [!question]- Que artigos a aula cita para a equipe técnica?
> Art. 7º (consentimento e transparência), art. 6º, IV (minimização), art. 46º (segurança e anonimização), arts. 18º e 20º (direitos), art. 48º (notificação de violação) e art. 14º (crianças e adolescentes).

> [!question]- Que tipos de medidas punitivas a LGPD prevê?
> Pecuniárias, administrativas ou penais.

## Aula 2 - Segurança dos dados
> [!question]- Quais as dez bases legais?
> Consentimento, legítimo interesse, contratos, obrigação legal, execução de políticas públicas, estudos por órgãos de pesquisa, processo judicial, proteção da vida, tutela de saúde e proteção de crédito. → [[Bases Legais da LGPD]]

> [!question]- Quais os quatro pilares?
> Legitimidade do interesse, necessidade, balanceamento e salvaguarda, com base na transparência.

> [!question]- Por que a aula 2 diz que a criptografia é "uma das soluções mais frágeis"?
> (O PDF não deixa claro se fala da assimétrica ou da criptografia em geral.) Porque, perdendo a chave, perde-se o acesso aos dados, e quem obtém a chave indevidamente acessa os dados.

> [!question]- At-rest × in-transit?
> Proteção no armazenamento (na fonte) e no transporte entre componentes; normalmente usadas juntas.

> [!question]- O que é anonimização, e ela é garantia absoluta?
> Transformar os dados para impossibilitar, de forma irreversível, a identificação do indivíduo. Não é garantia absoluta: técnicas avançadas podem, em alguns casos, reidentificar. → [[Anonimização de Dados]]

> [!question]- Cite processos de anonimização.
> Desfiguração, desconexão e sumarização.

## Aula 3 - Governança de dados
> [!question]- O que é governança de dados?
> Processos, responsabilidades, práticas e normas para gerenciar, proteger, disponibilizar e garantir a qualidade dos dados em todo o ciclo de vida. → [[Governança de Dados]]

> [!question]- De que duas maneiras a governança impacta as decisões?
> Guiando a tomada de decisão e lastreando (justificando) a decisão tomada.

> [!question]- Que boas ideias o PDF sugere para criar uma governança de dados?
> Organizar os dados existentes (classificar, documentar, mapear titulares e usuários), criar a estratégia de dados e implementar as ferramentas e a padronização.

> [!question]- Segurança × disponibilidade na governança?
> É mais importante que os dados estejam seguros do que disponíveis.

## Aula 4 - IA
> [!question]- Por que os cookies são ponto de atenção?
> Ficam no computador da pessoa; implementados de forma desleixada (ex.: sem criptografia), podem ajudar um invasor a obter dados sensíveis ou agir como o cliente. → [[Inteligência Artificial e LGPD]]

> [!question]- O que a organização deve informar para usar dados no treinamento de IA?
> O propósito, as mudanças de uso (permitindo negar) e que os dados serão usados para treinar modelos, com resultados que podem ser usados nos serviços.

> [!question]- O que é explicabilidade?
> A capacidade do modelo de explicar como chegou a uma inferência; muitas vezes exige entender os vieses pelos dados informados.

## Aula 5 - Implementação
> [!question]- No IaaS, de quem é a responsabilidade pela segurança?
> Em maior parte, da equipe técnica que implementa; o fornecedor responde só pelo funcionamento do recurso. → [[IaaS, PaaS e SaaS]]

> [!question]- No PaaS, quem responde por uma infração do terceiro?
> O operador dos dados, que continua responsável pelo uso e pela segurança.

> [!question]- Quais as cinco funções do NIST Cybersecurity Framework?
> Identificar, Proteger, Detectar, Responder e Recuperar. → [[NIST Cybersecurity Framework]]

## Aula 6 - Desenvolvimento
> [!question]- Privacidade por design × por padrão?
> Por design: privacidade em todas as fases, desde a concepção. Por padrão: no primeiro uso, as configurações mais restritas possíveis. → [[Privacidade por Design e por Padrão]]

> [!question]- Para que serve um cofre de senhas?
> Guardar os segredos fora do software, com rotação e troca de credenciais sem alterar o software, controle de acesso e registro de uso. → [[Cofre de Senhas]]

> [!question]- Por que a autorização deve ser validada no momento do uso?
> Porque a permissão pode ser revogada durante a sessão; vinculada ao login, a revogação demora muito mais. → [[Autenticação, Autorização e IAM]]

> [!question]- Como evitar dados reais em desenvolvimento?
> Anonimização ou mascaramento, bases com dados falsos (ex.: faker) e mascaramento dinâmico (o menos indicado; pode ser o único viável para erros difíceis de reproduzir).

## Aula 7 - Considerações finais
> [!question]- Quais os três agentes citados na aula 7?
> Controlador, operador e encarregado (interage com titulares e a autoridade nacional).

> [!question]- O que a LGPD diz sobre internacionalizar dados?
> Alguns tipos de dados não podem ser internacionalizados, mesmo que o operador externo esteja adequado.

> [!question]- Que papel tem quem desenvolve, e o que isso muda?
> Atua como operador de dados (aula 7; na aula 1, "geralmente", por criar, implantar e operar os sistemas); precisa atender aos requisitos de implementação e aos da LGPD.

## Pontos fracos
- 
