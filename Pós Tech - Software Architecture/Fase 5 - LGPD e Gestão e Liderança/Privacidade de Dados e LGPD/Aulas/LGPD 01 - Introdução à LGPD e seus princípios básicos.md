---
tags: [pos-tech/fase-5, lgpd, aula]
disciplina: Privacidade de Dados e LGPD
aula: 1
fonte: "Aula 01- Introdução à LGPD e seus princípios básicos.pdf"
---

# LGPD 01 - Introdução à LGPD e seus princípios básicos

[[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 02 - A segurança dos usuários e de seus dados]]

> [!summary] Em uma frase
> A **LGPD** protege os direitos fundamentais de **liberdade e privacidade** no tratamento de dados pessoais e vale para **todas** as empresas e organizações que tratam dados no Brasil. A aula apresenta o que a lei define (consentimento, finalidade, direitos dos titulares, segurança, prestação de contas), os **agentes de tratamento** (controlador e operador), os **direitos dos titulares**, o papel da **equipe técnica** (com os artigos da lei) e as **sanções**. Ver [[LGPD]].

## Hands On
Conhecer os docentes, o que a LGPD significa para quem cria e opera soluções de tecnologia, o que é a lei e os **papéis** de cada pessoa no âmbito dela.

## Por que importa
- Muitas empresas ainda adotam a LGPD mais como **obrigação contratual**, para continuar operando no ambiente digital, do que como preocupação genuína e ferramenta de segurança.
- Os dados pessoais não podem ser tratados como "mais uma informação": as pessoas, **donas de seus dados**, têm o direito de autorizar ou não o uso, e quem constrói e opera o software deve respeitar esse direito.

## O que é a LGPD
- Legislação brasileira que protege os direitos fundamentais de **liberdade e privacidade** dos cidadãos no tratamento de seus dados pessoais. Entrou em vigor em **18 de setembro de 2020**.
- Aplica-se a **todas as empresas e organizações** que coletam, armazenam, processam ou compartilham dados pessoais no Brasil, **independentemente de tamanho ou setor**, pessoas físicas ou jurídicas.
- Finalidade: resguardar **liberdade, privacidade e desenvolvimento individual** das pessoas naturais. Define o que são dados pessoais, os métodos de coleta e processamento, os direitos dos detentores e as **punições**.

## O que a LGPD define
| Ponto | O que o PDF diz |
|---|---|
| **Consentimento** | Exige o consentimento **explícito** para coletar e processar dados; deve ser **livre, informado e inequívoco** |
| **Finalidade e limitação** | Informar claramente a finalidade e não usar os dados para outros fins sem o consentimento do titular |
| **Direitos dos titulares** | Acessar, corrigir, excluir e portar os dados; revogar o consentimento |
| **Segurança e proteção** | Medidas **técnicas e organizacionais** contra acesso não autorizado, perda, alteração ou destruição |
| **Responsabilidade e prestação de contas** | Transparência nas práticas e capacidade de **demonstrar conformidade** |

**Obrigações das empresas**: responsabilizar-se pela segurança e privacidade dos dados · informar os titulares sobre a coleta e o tratamento · obter o consentimento · respeitar os princípios da **finalidade, necessidade, adequação, livre acesso, transparência, segurança, prevenção, não discriminação, responsabilização e prestação de contas**.

- A lei prevê a **ANPD** (Autoridade Nacional de Proteção de Dados), que fiscaliza e aplica sanções.

> [!note] Aqui o consentimento aparece como exigência geral; na aula 2, ele é uma das **dez bases legais** de tratamento (a mais comum). Ver [[Bases Legais da LGPD]].

## Agentes de tratamento
As partes envolvidas no ciclo de vida dos dados (quem coleta, processa, armazena e compartilha). Ver [[Agentes de Tratamento]].

| Papel | Quem é | Exemplo do PDF |
|---|---|---|
| **Controlador** | Decide quais dados coletar, como usá-los e com que propósito; **usualmente** o cliente ou a empresa que encomendou o software | A **loja** para a qual o time cria um app de compras |
| **Operador** | Lida efetivamente com os dados, seguindo as diretrizes do controlador | As pessoas dos times de **desenvolvimento**, de projeto de solução e de operações, que **geralmente** são operadoras |

## Direitos dos titulares
- O **titular** é quem usa o software: cliente, usuário ou pessoa registrada numa base por força de sua função (ex.: um empregado num sistema de gestão de pessoas). Ver [[Direitos dos Titulares]].
- Direitos: **acesso** · **retificação** · **anonimização, bloqueio ou eliminação** · **oposição** ao tratamento · **portabilidade** · **não ser submetido a decisões automatizadas**.

## O papel da equipe técnica
| Ponto | Artigo citado | O que fazer |
|---|---|---|
| **Consentimento e transparência** | Art. 7º | Consentimento **explícito e claro**; explicar de forma transparente por que os dados são coletados e como serão usados |
| **Minimização de dados** | Art. 6º, IV | Coletar só o **estritamente necessário**, o que ajuda os usuários a concordarem; evitar dados excessivos e sensíveis sem relação com a funcionalidade |
| **Segurança e anonimização** | Art. 46º | **Criptografia** no armazenamento e no transporte; considerar a **anonimização** sempre que possível |
| **Direitos dos usuários** | Arts. 18º e 20º | Funcionalidades para acessar, corrigir e excluir os dados; isso **pode** incluir interfaces para visualizar e gerenciar os dados |
| **Notificações de violação** | Art. 48º | Notificar os usuários e a **ANPD**; sistemas de segurança internos e externos para **detecção precoce** |
| **Dados de crianças e adolescentes** | Art. 14º | Consentimento **específico dos pais ou responsáveis** |

- A LGPD exige considerar privacidade e proteção **desde o início** do desenvolvimento.
- **A definir com o controlador**:
  - **Responsabilidades compartilhadas**: quem implementa e opera divide responsabilidades com o controlador (sistemas seguros, finalidade, direitos).
  - **Contratos de tratamento**: **geralmente** é necessário um contrato entre controlador e operador; **pode** incluir segurança, finalidades e direitos dos titulares.
  - **Privacidade por design**: privacidade desde o início, como requisito de **alta prioridade, mesmo que não funcional**; coleta minimizada e segurança no transporte, armazenamento e uso. Ver [[Privacidade por Design e por Padrão]].

## As empresas e a LGPD
- A não conformidade **pode** resultar em sanções, como multas e outras penalidades.
- **Exemplo**: no cadastro num serviço de **e-mail**, o fornecedor deve explicar de forma inequívoca como coleta e usa os dados; o indivíduo pode acessar, retificar, suprimir ou se opor, e alterar ou revogar a autorização a qualquer momento.
- As medidas punitivas **podem** ser **pecuniárias, administrativas ou penais**.

**Resumo rápido**: direitos e obrigações · consentimento explícito · acessar, corrigir, excluir e portar · segurança para **confidencialidade, integridade e disponibilidade** · multas significativas.

## O que você viu
A LGPD não é um problema: reforça a segurança dos dados, que sempre foi preocupação das empresas, e disciplina o uso por **recomendações e sanções**.

## Referências
AWS: Privacidade de dados no Brasil · Senado Notícias: LGPD entra em vigor · Brasil, Lei nº 13.709/2018 · Serpro: O que muda com a LGPD
