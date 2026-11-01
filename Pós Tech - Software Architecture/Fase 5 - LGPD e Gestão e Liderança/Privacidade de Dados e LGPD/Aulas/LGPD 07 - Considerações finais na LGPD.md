---
tags: [pos-tech/fase-5, lgpd, aula]
disciplina: Privacidade de Dados e LGPD
aula: 7
fonte: "Aula 07- Considerações finais na LGPD.pdf"
---

# LGPD 07 - Considerações finais na LGPD

← [[LGPD 06 - LGPD no desenvolvimento de software]] · [[Privacidade de Dados e LGPD]]

> [!summary] Em uma frase
> Revisão geral da disciplina: a lei (de **14 de agosto de 2018**, regulada pela **ANPD**), o consentimento e os direitos do titular, os **três agentes** (controlador, operador e **encarregado**), a **anonimização**, as bases legais e seus quatro pilares, a governança de dados, a proteção (controle de acesso e criptografia), a IA, os projetos com serviços de nuvem e o desenvolvimento de software. Muitas práticas **já existiam**, mas por falta de regulação não eram seguidas.

## Hands On
Recapitular as aulas anteriores e discutir como a LGPD pode ser a **base de uma política de dados** da organização.

## A lei
- **Lei de 14 de agosto de 2018**, regulada pela **ANPD**; cria um cenário de **segurança jurídica** para os dados de todo cidadão que esteja no Brasil e protege **liberdade, privacidade e o livre desenvolvimento da personalidade**. Ver [[LGPD]].
> [!note] Aqui o consentimento aparece como necessário para usar os dados; mais adiante, a própria aula o trata como o "caso comum" entre as bases legais.

- Para usar os dados, a organização precisa do **consentimento** do titular, que pode ser **alterado ou revogado** a qualquer momento. O titular também pode pedir a **exclusão**. A organização deve fornecer ferramentas e processos para o titular saber como os dados são usados e pedir revogação ou exclusão.

| Agente | Papel ([[Agentes de Tratamento]]) |
|---|---|
| **Controlador** | Define como os dados devem ser tratados |
| **Operador** | Executa o tratamento **em nome do controlador** e sob sua orientação |
| **Encarregado** | Interage com os **titulares** e a **autoridade nacional** |

- A **ANPD** fiscaliza e aplica as penas.

> [!note] O encarregado aparece pela primeira vez nesta aula; a aula 1 só trata de controlador e operador.

## Anonimização
- Os dados anonimizados **não fazem parte do escopo** da LGPD: caracterizam um indivíduo sem **particularizá-lo**. **Exemplo**: "uma mulher negra de 30 anos, moradora de Belo Horizonte" descreve um grupo, mas não identifica individualmente ninguém. Ver [[Anonimização de Dados]].

> [!note] Aqui os anonimizados não permitem identificar **diretamente** o cidadão; na aula 2, a anonimização impede a identificação **direta ou indireta**.
- "Ainda assim, alguns dos dados anonimizados são considerados **sensíveis**", segundo a lei (**art. 5, II**): origem racial ou étnica, convicção religiosa, opinião política, filiação a sindicato ou organização religiosa, filosófica ou política, dado de saúde ou vida sexual, dado genético ou biométrico. A lei também resguarda os direitos de **crianças e adolescentes**.
- Muito usados para entender o **perfil de navegação** e em **propagandas direcionadas**, mas **podem** ser usados para manipulação de grupos ou crimes, racismo ou LGBTQIA+fobia.

> [!warning] A aula diz que os dados anonimizados ficam **fora do escopo** da LGPD e, logo depois, que alguns deles são **sensíveis** pela lei; o trecho citado do art. 5, II é a lista de dados sensíveis.

## Segurança de dados e bases legais
- A organização se preocupa não só com armazenamento e transferência, mas com o **uso** e como ele é feito.
- **Bases legais**: o consentimento é o **caso comum**; outras são legítimo interesse, contratos, obrigações legais, políticas públicas, estudos por órgãos de pesquisa, processo judicial, proteção da vida, tutela de saúde e proteção de crédito. Ver [[Bases Legais da LGPD]].
- **Quatro pilares**: **legítimo interesse** da organização e do titular · **necessidade** para uma finalidade exposta e acordada · **balanceamento** (uso adequado) · **salvaguarda** (recursos do titular para acompanhar e alterar o acesso). Tudo com **transparência** clara, explícita e inequívoca.

## Governança de dados
Conjunto de decisões e responsabilidades implícitas e explícitas que dá suporte a políticas e práticas que definem, de forma inequívoca, como a organização se comporta em relação aos dados. Não se baseia só na LGPD: é "um guia de como a empresa usa, protege, opera e valoriza os dados". Ver [[Governança de Dados]].

## Proteção dos dados
Acontece no **armazenamento (at-rest)** ou na **transferência (on-transit)**; duas estratégias se sobressaem:
- **Controle de acesso**: conforme a política da governança; entrega ao requisitante (pessoa ou software) só o formato e o conjunto **necessários**: **minimização do acesso**, dados **anonimizados ou consolidados** e **ocultação** de dados sensíveis.
- **Criptografia**: transformar legível em ilegível e vice-versa; amplamente usada e "um modo seguro" de armazenamento e transporte. Ver [[Criptografia e mTLS]].

> [!note] Na aula 2, a criptografia é também "uma das soluções mais frágeis"; na aula 6, "forma inicial de proteção baseada em ofuscamento".

> [!note] Nesta aula a transferência aparece como "**on**-transit"; na aula 2, "**in**-transit".

## Inteligência artificial
- Os dados são usados em dois momentos: no **treinamento** e na **geração das predições**. Mais dados **tendem** a modelos mais assertivos. Ver [[Inteligência Artificial e LGPD]].
- Informar, **no momento do consentimento**, que os dados podem ser usados para treinar modelos e gerar recomendações.
- Dados **anonimizados ou consolidados** **permitem** treinar sem identificar diretamente os titulares; **testar vieses e desvios** nas predições é importante.

## Projetos de TI e serviços de nuvem
- Serviços pagos por consumo, de **Infraestrutura, Plataforma e Serviço**, de grandes fornecedores (AWS, Microsoft, Google) a operações especializadas. Ver [[IaaS, PaaS e SaaS]].
- **Desafios**: entender como o fornecedor implementa a segurança e se adequa à LGPD; com serviços **fora do Brasil**, a LGPD define que **alguns tipos de dados não podem ser internacionalizados**, mesmo que o operador externo esteja adequado.
- O nível de responsabilidade **usualmente** se relaciona à **autonomia** sobre o componente. **Exemplo**: num **MySQL como plataforma**, a responsabilidade é no nível do banco (estrutura, armazenamento, gestão de acesso); o entorno (manutenção do software, segurança da rede) é do fornecedor.

## Desenvolvimento de software
- Quem desenvolve atua como **operador de dados**; precisa atender aos requisitos de implementação **e** aos da LGPD.
- A governança define o limite de responsabilidade e o acesso aos dados para desenvolver e testar, e o acesso do software em operação; é **responsabilidade do software** fazer isso funcionar.
- **Privacidade por design** (requisito fundamental em todas as fases) e **por padrão** (todas as configurações de segurança ativadas, a menor quantidade possível de dados). Ver [[Privacidade por Design e por Padrão]].
- **Configurações** segregadas em lugar seguro: mudar a configuração remotamente ou invalidar um acesso suspeito; **centralizar** a validação de identidade em soluções de autenticação e autorização ([[Autenticação, Autorização e IAM]]).

## O que você viu
A LGPD já é realidade; muitas práticas de segurança **já existiam**, mas não eram seguidas por falta de regulação. Cabe a cada pessoa entender como a lei impacta seu trabalho, o negócio e seu dia a dia **como titular de dados**.

## Referências
Fabor: a pessoa anônima e a LGPD · MPF: O que é a LGPD · Planalto: Lei nº 13.709/2018 · Serpro: Serpro e LGPD · Silva: privacidade, algoritmos inteligentes e futuro
