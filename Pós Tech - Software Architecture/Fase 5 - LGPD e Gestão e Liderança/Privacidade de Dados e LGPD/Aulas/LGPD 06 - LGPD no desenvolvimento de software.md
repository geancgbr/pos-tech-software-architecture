---
tags: [pos-tech/fase-5, lgpd, aula]
disciplina: Privacidade de Dados e LGPD
aula: 6
fonte: "Aula 06- LGPD no desenvolvimento de software.pdf"
---

# LGPD 06 - LGPD no desenvolvimento de software

← [[LGPD 05 - LGPD na implementação da solução de tecnologia]] · [[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 07 - Considerações finais na LGPD]]

> [!summary] Em uma frase
> A LGPD aumenta a responsabilidade de quem constrói software. A aula parte da **privacidade por design** e **por padrão**, trata da **criptografia at-rest e in-transit** e de ferramentas de apoio (**cofres de senha**, **autenticação, autorização e IAM**, **armazenamento de configurações**) e de como proteger os **ambientes de desenvolvimento** (anonimização ou mascaramento, bases com dados falsos, mascaramento dinâmico).

## Hands On
Os principais pontos de atenção ao construir software de acordo com a LGPD, com exemplos: a complexidade aumenta, mas há **ferramentas** que ajudam.

## Privacidade na criação do software
Ver [[Privacidade por Design e por Padrão]].
| | **Privacidade por design** | **Privacidade por padrão** |
|---|---|---|
| O que é | Integrar os princípios de privacidade em **todas as fases** do ciclo de desenvolvimento; não uma camada extra, mas um elemento fundamental **desde a concepção**, como um dos principais requisitos | Definir, no **primeiro uso**, todas as configurações de segurança como **as mais restritas possíveis**: sem intervenção do usuário, minimizar a coleta, limitar a divulgação e restringir o acesso |
| Efeitos | **Tende** a reduzir os riscos de violação (vulnerabilidades tratadas de forma proativa, no código); as empresas **podem** ganhar a confiança dos usuários e mostrar atenção às leis | Funcionalidades pensadas para usar só a quantidade necessária de dados, da interface aos componentes mais complexos; dificultar processos que possam causar falhas e, se o usuário os executar, ter **evidências** de que foi a ação dele |

- Muitos usuários **podem não** saber ajustar a privacidade; protegê-los desde o início dá a sensação de segurança. **Muitas vezes** é conhecido como **"proteger o usuário de si mesmo"**: restrições contra problemas por **imperícia ou má-fé**.

## Criptografia
- Codificar caracteres para que não sejam entendidos sem o mecanismo de interpretação; uma forma inicial de proteção baseada em **ofuscamento**. Ver [[Criptografia e mTLS]].
- **Dois tipos principais**: em armazenamento e em trânsito; não dá para cuidar de um só (dados seguros no armazenamento e inseguros no trânsito podem ser explorados por softwares de **escuta**).

| | **At-rest** (em descanso) | **In-transit** (em trânsito) |
|---|---|---|
| Protege | Dados em mídia persistente: disco, tabelas de banco, armazenamento em nuvem | Dados transferidos entre servidores, dispositivos ou redes |
| Efeito | Quem acessa os dados não os lê sem a **chave** ou a tecnologia usada; o tipo **mais conhecido** | Dados capturados aparecem ininteligíveis; exemplo: **HTTPS**, camada de segurança sobre o HTTP |
| Problemas / ressalvas | Gerenciar as **chaves** com segurança; **perder a chave** torna os dados inúteis; **tende** a consumir muito processamento, impactando ambientes limitados | Não é transmitir dados criptografados, mas **criptografar o transporte**; **muitas vezes** podemos confiar na infraestrutura (o PDF cita as aplicações em http), mas isso **pode ser considerado** um **risco calculado**: parte-se da **premissa** de que o software só é seguro em ambiente compatível |

> [!note] O exemplo de criptografia em trânsito é o **HTTPS**, mas logo depois o texto fala em "aplicações que se comunicam pelo protocolo **http**" e diz que não se trata de "transmissão de dados criptografados".

## Ferramentas de apoio
### Cofres de senha
- Armazenam credenciais ("**segredos**") de serviços, de forma que o software **não as armazene**, e permitem **rotação** de senhas e mudança de credenciais **sem alterar o software**. Ver [[Cofre de Senhas]].
- **Podem** gerenciar o acesso aos segredos (**mínimo privilégio**), **registram** quando e por quem foram usados e permitem renovar ou revogar credenciais; em cloud, **podem** ser integrados para rotacionar automaticamente.
- **Exemplo**: cofre + rotação de credenciais garante acesso restrito a quem precisa e **por um tempo curto** (o tempo de rotação); a ferramenta troca a senha no serviço (ex.: banco de dados) e entrega a senha válida.

### Autenticação, autorização e gerenciamento de identidade
Ver [[Autenticação, Autorização e IAM]].
| | **Autenticação** | **Autorização** |
|---|---|---|
| Pergunta | "Você é realmente quem diz ser?" | "O que você está autorizado a fazer aqui?" |
| Como | **Frequentemente** usuário e senha; em sistemas mais seguros, **múltiplos fatores** (tokens, biometria, códigos por SMS, e-mail ou app) | Permissões a um usuário (humano ou software) **já autenticado**; ex.: ler um documento, mas não editá-lo |
| Segurança | Cria uma **sessão de uso**, que **pode** ter tempo de vida limitado ou máximo de sessões por identidade; a identidade é validada constantemente, minimizando compartilhamento de senha e sessões longas | Validada **sempre no momento do uso**: a permissão pode ser revogada durante a sessão; se vinculada ao **login**, a revogação demora muito mais |

- **IAM** (Identity and Access Management): criação, manutenção e exclusão de identidades de forma **centralizada e segregada** das aplicações; **fonte única** de dados confiáveis para vários serviços, com identificação por **ferramentas** confiáveis operadas por um terceiro especializado, com acesso conforme padrões predefinidos.
- O IAM virou parte da **estratégia de segurança**: a responsabilidade de quem constrói software agora é "implementar o que o limite de acesso impõe, e nada mais".

### Armazenamento de configurações
- Junto aos cofres, guarda dados de aplicação **não sensíveis** fora do software: se o código-fonte for obtido ilicitamente, nenhuma configuração vaza.
- Permite alterar configurações **sob demanda** (ex.: desativar um software com mau funcionamento que vaza dados mudando uma configuração).
- Permite **ambientes de execução segregados**: o mesmo software obtém as configurações do seu ambiente e pode ser testado em ambientes adaptados.

## Ambientes de desenvolvimento
- Quem desenvolve **usualmente** prefere dados reais, cópias deles ou até **conexão direta** ao banco operacional. É mais comum do que deveria e configura **falha grave**: mesmo num ambiente teoricamente protegido, **pode** configurar risco grave à integridade e ao direito de uso pela LGPD.

| Técnica | O que o PDF diz |
|---|---|
| **Anonimização ou mascaramento** | Ferramentas transformam os dados no transporte entre ambientes, mantendo os **tipos**, mas sem relacioná-los aos donos |
| **Bases baseadas em perfis** | Dados **falsos** (ex.: a biblioteca **"faker"** do Python) num banco com a mesma estrutura e características semelhantes (quantidade de tabelas e registros, perfis de busca e desempenho) |
| **Mascaramento dinâmico** | Para reproduzir e corrigir erros quando dados reais são imprescindíveis: só os dados necessários ao processo. A **menos indicada** (complexidade e risco), mas **pode** ser a única viável para problemas de alta complexidade de reprodução |

Ver [[Anonimização de Dados]].

## O que você viu
A LGPD torna a construção de software mais complexa, mas isso **pode** ser visto como oportunidade para criar práticas de controle de acesso e manuseio de dados, como garantia de **segurança e confiabilidade**.

## Referências
AWS: IAM · Delphix: mascaramento de dados · GAT InfoSec: Security by Design · Google Cloud: O que é criptografia · Stefanini: anonimização · Tripla: Privacy by Design e Privacy by Default
