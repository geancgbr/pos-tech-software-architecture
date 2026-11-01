---
tags: [pos-tech/fase-5, lgpd, aula]
disciplina: Privacidade de Dados e LGPD
aula: 2
fonte: "Aula 02- A segurança dos usuários e de seus dados.pdf"
---

# LGPD 02 - A segurança dos usuários e de seus dados

← [[LGPD 01 - Introdução à LGPD e seus princípios básicos]] · [[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 03 - Governança de dados]]

> [!summary] Em uma frase
> A segurança de dados da organização viabiliza sua operação; a LGPD é um **conjunto de regras adicionais** a seguir sob pena de punição. A aula traz as **dez bases legais** e seus **quatro pilares** (legitimidade do interesse, necessidade, balanceamento, salvaguarda), os processos técnicos de segurança, a proteção dos dados (**criptografia, autenticação e autorização, minimização, atualização e treinamento**, at-rest e in-transit) e a **anonimização**.

## Hands On
Segurança de dados na organização: preocupações iniciais, definição e implementação da **política de dados**, à luz da LGPD e de outras leis.

## Segurança de usuários e de seus dados
- Conjunto de medidas que protegem as informações pessoais contra **acesso não autorizado, uso indevido, divulgação, alteração ou destruição**.
- No Brasil, é regulamentada pela LGPD, que, segundo esta aula, entrou em vigor em **agosto de 2020**.
- **Direitos** (para o benefício dos cidadãos): acesso, retificação, apagamento, portabilidade e revogação da concessão de acesso. **Obrigações**: informar como e por quem os dados são tratados; protegê-los; responder a solicitações de acesso, retificação, apagamento e portabilidade.
- Refere-se à proteção das informações **pessoais e sensíveis** de quem usa serviços online, aplicativos, websites e outras plataformas.

> [!warning] A aula 1 diz que a LGPD entrou em vigor em **18 de setembro de 2020**; esta aula (e as aulas 3 e 4) diz **agosto de 2020**.

## Bases legais
São **dez** bases legais de autorização de tratamento. Ver [[Bases Legais da LGPD]].

| # | Base legal | O que o PDF diz |
|---|---|---|
| 1 | **Consentimento** | Declaração clara e inequívoca de concordância; a **mais comum**, quando a empresa precisa dos dados para prestar um serviço |
| 2 | **Legítimo interesse** | Anuência baseada em **interesse mútuo**: o dono aceita o uso em troca de alguma vantagem |
| 3 | **Contratos** | Concordar com o uso, por força de um contrato, para cumprir o objeto do contrato |
| 4 | **Obrigação legal** | Forçado **por lei** a compartilhar, sem direito sobre o uso |
| 5 | **Execução de políticas públicas** | Forçado pela aplicação de políticas públicas, sem direito sobre o uso |
| 6 | **Estudos por órgãos de pesquisa** | O dono **pode optar** por compartilhar com institutos de pesquisa, de boa-fé; **normalmente** para traçar perfis de populações, de forma **anonimizada** |
| 7 | **Processo judicial** | Forçado por lei a compartilhar, sem direito sobre o uso |
| 8 | **Proteção da vida** | Interesse **vital** do titular, de dependentes ou de pessoa diretamente ligada |
| 9 | **Tutela de saúde** | Uso por profissionais ou serviços de saúde ou autoridade sanitária |
| 10 | **Proteção de crédito** | O titular **pode** permitir o uso para **análise de crédito** ou garantia de confiabilidade de transação |

**Quatro pilares** a que as bases podem ser reduzidas:
| Pilar | O que o PDF diz |
|---|---|
| **Legitimidade do interesse** | A organização define o uso, a importância e a finalidade; entendidos por todas as partes, o interesse é existente e válido |
| **Necessidade** | Os dados são necessários para a finalidade acordada; o **conjunto mínimo** e as bases de avaliação dele; só captar o necessário ao escopo |
| **Balanceamento** | Avaliar se o uso garante tratamento adequado ao dono (ex.: perfilamento **invasivo** ou categorização **discriminatória**) |
| **Salvaguarda** | O dono tem recursos para garantir as regras e **alterar** os dados ou **revogar** o acesso quando quiser |

- Tudo com base na **transparência**: de forma clara, explícita e inequívoca, como os dados serão armazenados, processados, usados e, se fizer sentido, compartilhados com terceiros.

## Processos técnicos de segurança
- A política de segurança **usualmente** se baseia em **implantação, monitoramento e auditoria** de processos técnicos, que visam **burocratizar e dificultar** todo acesso aos dados, para demonstrar que a segurança está sendo aplicada.
- Duas frentes: **ferramentas** de tecnologia que aplicam as regras e **políticas internas** operadas por profissionais que decidem quem (pessoas ou ferramentas) acessa quais dados e de que forma, com base nas orientações da companhia, no negócio e em boas práticas.

## Proteção dos dados
Em sua maioria soluções técnicas, mas **muitas vezes podem não ser as únicas**.

| Medida | O que o PDF diz |
|---|---|
| **Criptografia** | Transforma informações legíveis em **texto cifrado** com algoritmos; só quem tem a **chave** decifra. Hoje, o modo mais seguro de transporte e armazenamento é a **assimétrica** (uma chave cifra, outra decifra). Mas é também **uma das soluções mais frágeis**: perder a chave é perder os dados, e quem obtém a chave acessa os dados. Ver [[Criptografia e mTLS]] |
| **Autenticação e autorização** | **Autenticação**: garantir a identidade (senha, biometria, chave física). **Autorização**: acesso apenas aos dados esperados, conforme necessidade, atuação e responsabilidade. A burocratização acontece, em grande parte, aqui |
| **Minimização de acesso** | Coletar só o necessário: "Se você não precisa de algumas informações, não as colete" |
| **Atualização de softwares e treinamento** | Manter os serviços atualizados minimiza disrupções; a equipe deve ser treinada para trabalhar com os dados e tomar decisões alinhadas à política, dentro da conformidade |

> [!warning] A avaliação da criptografia muda: aqui é "o modo mais seguro" e, no mesmo parágrafo, "uma das soluções mais frágeis" (o sujeito é ambíguo: a assimétrica ou a criptografia em geral); na aula 6, "forma inicial de proteção baseada em ofuscamento"; na aula 7, "um modo seguro".

- A proteção acontece em **dois momentos**: no **armazenamento (at-rest)** e no **transporte (in-transit)**; não são excludentes e **normalmente** são usados juntos.

> [!note] O item se chama "minimização de **acesso**", mas descreve reduzir os dados **coletados**.

## Anonimização
- Transformar dados pessoais para **impossibilitar a identificação direta ou indireta** de um indivíduo, de forma **irreversível**, mesmo combinando com outras informações. Ver [[Anonimização de Dados]].
- A LGPD considera os dados anonimizados **fora da definição de dados pessoais**, sem as mesmas regras de proteção e consentimento.
- Não é **garantia absoluta**: técnicas avançadas **podem**, em alguns casos, permitir a reidentificação; deve ser feita com rigor.
- Os processos dependem do contexto; exemplos: **desfiguração** (alterar para não identificar as pessoas), **desconexão** (dividir em unidades de armazenamento, como tabelas, quebrando a relação) e **sumarização** (entregar pré-processado, só com o necessário).

## O que você viu
A segurança de dados não é só no servidor ou no transporte: a LGPD impõe cuidados no **acesso e tratamento** e força a pensar regras da lei como **funcionalidades** para os donos dos dados, como **revogação** de concessão e **auditoria** de uso.

## Referências
AWS: Privacidade de dados no Brasil · Gonçalves: bases legais da LGPD · Nones: o que diz a LGPD · Planalto: Lei nº 13.709/2018 · Senado Notícias · Serpro
