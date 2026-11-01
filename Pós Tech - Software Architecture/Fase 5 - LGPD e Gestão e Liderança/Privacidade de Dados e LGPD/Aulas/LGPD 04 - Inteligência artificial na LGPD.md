---
tags: [pos-tech/fase-5, lgpd, ia, aula]
disciplina: Privacidade de Dados e LGPD
aula: 4
fonte: "Aula 04- Inteligência artificial na LGPD.pdf"
---

# LGPD 04 - Inteligência artificial na LGPD

← [[LGPD 03 - Governança de dados]] · [[Privacidade de Dados e LGPD]] · Próxima → [[LGPD 05 - LGPD na implementação da solução de tecnologia]]

> [!summary] Em uma frase
> Os modelos de **IA** são treinados com dados que **usualmente** vêm dos usuários atuais do software. A LGPD **restringe** esse uso: é preciso informar o propósito, obter consentimento, avisar mudanças e dizer que os dados serão usados para **treinar modelos**. A aula trata da coleta (formulários e **cookies**), das aplicações da IA e das práticas de **ética e transparência**, como a **explicabilidade**. Ver [[Inteligência Artificial e LGPD]].

## Hands On
O que é IA, por que ela precisa dos dados de usuários, onde e como a LGPD limita o acesso e tenta regimentar o uso para treinamento, e quando o uso vira **invasão de privacidade**.

## Por que a IA precisa de dados
- Com os dados dos usuários, as ferramentas **podem** identificar **padrões de consumo**, correlacionam grandes volumes e entregam ofertas com maior potencial de aquisição.
- Perguntas da aula: qual o limite de uso dos dados por essas ferramentas? Qual o papel da LGPD? Quais os limites para oferecer algo a um potencial cliente?
- A **IA** é a área da ciência da computação que se concentra na criação de **sistemas inteligentes**.

## Coleta de dados de usuários
- Dados coletados ao usar produtos ou serviços digitais, **majoritariamente** sites e aplicativos; **podem** incluir nome, endereço, e-mail e histórico de navegação.
- **Exemplo**: ao se inscrever num serviço, o usuário fornece nome, endereço e e-mail, em troca de algum **possível benefício futuro**.

## Cookies e a IA
- Pequenos arquivos armazenados no computador do usuário quando ele visita um site. Criados para manter informações no site, passaram a armazenar dados **mais avançados** sobre os indivíduos.
- São um dos principais **pontos de atenção** na segurança: num ataque ao browser, se implementados de forma **desleixada** (ex.: sem criptografia), **podem** ajudar o invasor a obter dados sensíveis ou a **agir como o cliente**.
- Permitem rastrear o comportamento (páginas visitadas, produtos vistos, itens comprados). Com um modelo de IA, é possível moldar **em tempo real** a experiência: facilidades de navegação, ofertas adequadas, uma lista de compras baseada na navegação em um ou mais sites.

## IA e o uso de dados para treinamento
- O avanço da IA depende de **extensos conjuntos de dados**. Os dados de usuários são fundamentais no treinamento de modelos de IA, que **podem** ser usados para interpretar textos, contextos e até **sentimentos**; são a base de assistentes virtuais e chatbots baseados em **LLM** (Large Language Model).
- As organizações **podem**, a princípio, usar os dados em sua posse: confiáveis, de interações reais. **Exemplo**: modelar as compras de uma mulher de 30 anos com salário entre 4.000 e 6.000 reais é mais simples com dados desse perfil.
- Mas esse uso, por imposição da LGPD, é **restrito**.

## A LGPD e o uso dos dados
Com a LGPD (aqui, "agosto de 2020"), algumas considerações:
- **Antes** de coletar ou processar: informar o propósito e obter **consentimento explícito** (como na aula 1, uma exigência geral; ver [[Bases Legais da LGPD]]); permitir acessar, corrigir e excluir; investir em segurança contra vazamentos e mau uso.
- **Informar mudanças** no uso e permitir **negar** o uso: os dados estão disponíveis para um uso específico num contexto específico, como combinado na permissão.
- **Informar que os dados serão usados para treinar modelos de IA** e que os resultados **podem** ser usados na prestação de serviços, mostrando o benefício **indireto** ao indivíduo (ex.: possível oferta de um bem ou serviço).

## Como a IA pode ser usada
Usada de forma **ética e responsável**:
| Aplicação | O que o PDF diz |
|---|---|
| **Sistemas de recomendação** | Sugerir conteúdo ou produtos pelo perfil, comparando com perfis semelhantes |
| **Marketing digital** | Atingir o público-alvo de forma mais assertiva; dados do público como parâmetros da publicidade direcionada |
| **Pesquisa inteligente** | Filtrar e encontrar informações em vastos bancos de dados |
| **Personalização da experiência** | Adaptar interfaces a partir de interações passadas |
| **Segurança cibernética** | Detecção proativa de ameaças e fraudes, identificando padrões suspeitos |

## Ética e transparência
- A **ética** é o conjunto de princípios que orientam o comportamento da organização; é **particular a cada organização**.

| Prática | O que o PDF diz |
|---|---|
| **Transparência e explicabilidade** | Compreender como a IA toma decisões. A **explicabilidade** é a capacidade do modelo de explicar como chegou a uma **inferência**; muitas vezes não é possível só com ferramentas: é preciso entender, pelos dados informados, os **vieses** e seu impacto |
| **Entendimentos éticos** | Os profissionais devem entender os princípios que guiam projeto, desenvolvimento e implementação |
| **Tomada de decisões éticas** | Evitar discriminações, proteger a privacidade, garantir segurança e transparência |
| **Garantia de privacidade** | Proteção dos dados e conformidade com leis como a LGPD |
| **Monitoramento e auditoria** | Para a conformidade com as políticas de segurança e privacidade |
| **Aplicação de princípios éticos** | Em todas as áreas, da concepção à manutenção |

## O que você viu
- A LGPD não deve ser vista **meramente como obstáculo**: estabelece um marco regulatório com diretrizes claras e sanções.
- A convergência entre LGPD e IA ocorre no **treinamento**: quais dados, como, com que objetivo e qual o uso do resultado, à luz da LGPD, da **governança de dados** da empresa e de seus **princípios éticos**.

## Referências
AWS: Privacidade de dados no Brasil · Faceli et al., *Inteligência Artificial, Aprendizado de Máquina e Robótica* · Nunes e Morato: explicabilidade da IA · Planalto: Lei nº 13.709/2018 · Rhaman, *Inteligência artificial e aprendizado de máquina* · Senado Notícias · Serpro
