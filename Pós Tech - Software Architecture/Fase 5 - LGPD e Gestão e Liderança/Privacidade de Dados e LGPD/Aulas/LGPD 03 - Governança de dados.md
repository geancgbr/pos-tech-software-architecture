---
tags: [pos-tech/fase-5, lgpd, governanca, aula]
disciplina: Privacidade de Dados e LGPD
aula: 3
fonte: "Aula 03- Governança de dados.pdf"
---

# LGPD 03 - Governança de dados

← [[LGPD 02 - A segurança dos usuários e de seus dados]] · [[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 04 - Inteligência artificial na LGPD]]

> [!summary] Em uma frase
> A **governança de dados** é a estrutura que guia como os dados são tratados na empresa (organização, classificação, armazenamento e acesso): processos, responsabilidades, práticas e normas para gerenciar, proteger, disponibilizar e garantir a qualidade dos dados ao longo do **ciclo de vida**. Ela se alinha à LGPD, que **pode** ser vista como um novo "interessado" e uma **base legal** para criá-la. Ver [[Governança de Dados]].

## Hands On (vídeo)
- A definição da governança de dados é feita **fora do time de tecnologia**: a adoção não é voluntária, e cabe à TI **apenas implementar** o que foi definido.
- Na videoaula: o que é, que preocupações e motivações guiam a definição e como ela impacta a equipe de TI e o desenvolvimento.

## Contexto
- Com a transformação digital e leis como a LGPD, a governança de dados tem **importância fundamental**; ajuda a garantir **qualidade, segurança e privacidade**.
- Implementá-la é um desafio: profissionais de TI precisam integrar esses princípios e implementar regras que **podem inviabilizar** o funcionamento da solução.
- Os dados são um **ativo crucial**: orientam decisões, otimizam operações e **podem** ser a diferença entre sucesso e fracasso.

## O que é governança
- O conjunto de **decisões e responsabilidades explícitas e implícitas** de uma organização com clientes, parceiros e sociedade; um guia para a tomada de decisões.
- Impacta as decisões de duas maneiras: **guia** a decisão e **lastreia** (justifica) a decisão tomada.
- Bem definida, todos (clientes, investidores, parceiros, funcionários) sabem como e por que a organização funciona assim; **não há espaço para ambiguidade nem indecisão**.

## Governança de dados
- Processos, responsabilidades, práticas e normas para **gerenciar, proteger, disponibilizar e garantir a qualidade** dos dados: como são coletados, armazenados, utilizados e eliminados.
- **Não é puramente técnica**: confluência de gestão, processos organizacionais, políticas, padrões e tecnologia. O produto principal é um conjunto de **políticas e práticas** para todo o **ciclo de vida** (criação e coleta → armazenamento, acesso, compartilhamento → arquivamento ou exclusão).

| Componente | O que o PDF diz |
|---|---|
| **Padronização e qualidade** | Dados consistentes e confiáveis, com padrões definidos |
| **Integridade** | Precisos e completos, sem duplicatas ou inconsistências |
| **Segurança** | Proteção contra acesso não autorizado, corrupção ou perda: criptografia, controle de acesso, auditorias e backup |
| **Privacidade e conformidade** | De acordo com leis locais ou internacionais, como o **GDPR** |
| **Arquitetura e integração** | Como os dados são estruturados, armazenados, integrados e fluem pelos sistemas |
| **Gestão de metadados** | Origem, relacionamentos, definições e uso dos dados |
| **Linha do tempo e ciclo de vida** | Quanto tempo são retidos e quando e como são arquivados ou excluídos |
| **Stakeholders e responsabilidades** | Quem responde por quê; **pode** envolver papéis como **"steward" de dados**, **dono de dados** e **consumidores de dados** |

| Benefícios | Riscos de uma governança inadequada |
|---|---|
| **Conformidade legal** (ex.: LGPD), evitando penalidades · **tomada de decisão aprimorada** · **reputação fortalecida** | **Sanções e multas** · **danos à reputação** · **decisões ineficazes** por insights imprecisos |

## Governança de dados e a LGPD
- Alinha-se à LGPD ao garantir os **princípios da lei** (transparência, finalidade, necessidade etc.), fortalecendo a confiança de clientes e parcerias.
- **Vantagem**: basear parte da governança nos limites da LGPD, porque **algumas regras são automáticas e indiscutíveis**. Em torno delas se constrói uma estrutura que atende aos interessados (clientes, parceiros, investidores) e regula quem opera os dados (funcionários, parceiros de operação).

> [!note] A aula repete, quase igual, o trecho da aula 2 sobre segurança dos usuários (medidas, direitos, obrigações e vigência em agosto de 2020).

## Como criar uma governança de dados
Não é simples: depende da **cultura**, dos **objetivos de negócio** e de como a organização entende que deve funcionar. A LGPD não é o único pilar; o PDF sugere "algumas **boas ideias que podem ser utilizadas**":

1. **Organizar os dados existentes**: classificar, documentar e entender seu papel no negócio; identificar os **titulares e usuários** dos dados. "Usuários" são as pessoas ou softwares que acessam e manipulam os dados; mapear que dados acessam, **como** acessam e usam.
2. **Criar a estratégia de dados**: olha para o futuro (como os dados serão usados, armazenados e acessados); é a base do **grupo de políticas**, e dele saem os processos e práticas. "Sem saber por qual motivo um processo precisa ser implementado não é possível tomar nenhuma decisão técnica."
3. **Implementar as ferramentas**: a **padronização** dos dados e do acesso é ponto sensível, porque pessoas **podem perder acesso** e softwares **podem parar de funcionar**. Esse pior cenário deve ser documentado; no conflito de interesses, são postos à prova o **apoio das esferas superiores** e a **qualidade das ferramentas**.

- Na segurança de dados, é **mais importante que os dados estejam seguros do que disponíveis**; se algum ponto da organização se opõe, é preciso repensar a governança.
- O nível de governança deve ser **adequado** à organização e aos donos dos dados. Envolver muitas pessoas cria **responsabilidade compartilhada**; sem isso, os dados ficam "atrás de mais burocracia".

> [!note] O PDF diz que os titulares e usuários dos dados "são os que representam os controladores e operadores de dados"; na aula 1, o titular é a pessoa dona dos dados, distinta do controlador e do operador.

## O que você viu
A governança de dados é **anterior à LGPD**, pela natureza burocrática das empresas. A LGPD define novas regras e **pode** ser vista como um novo "interessado"; a governança é, ao mesmo tempo, a definição de um processo e a implementação de políticas para vários interessados.

## Referências
Da Silva (Alura): O que é Governança de Dados · IBGC: Governança Corporativa · Locus Iuris: governança de dados e LGPD · Opus Software · Planalto: Lei nº 13.709/2018
