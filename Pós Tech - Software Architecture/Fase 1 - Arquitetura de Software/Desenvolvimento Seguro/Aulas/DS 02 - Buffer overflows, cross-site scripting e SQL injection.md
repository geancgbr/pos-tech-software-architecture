---
tags: [pos-tech/fase-1, seguranca, aula]
disciplina: Desenvolvimento Seguro
aula: 2
fonte: "Aula 2.pdf"
---

# DS 02 - Buffer overflows, cross-site scripting e SQL injection

← [[DS 01 - Vulnerabilidades, ataques e intrusões]] · [[Desenvolvimento Seguro]] · Próxima → [[DS 03 - Bibliotecas de software]]

> [!summary] Em uma frase
> Alguns ataques são comuns e evitáveis, como DDoS, SQL Injection, Command Injection e XSS. A aula organiza os [[Tipos de Ataques|principais ataques a servidores]] em 7 categorias e mostra casos famosos de [[SQL Injection e Command Injection|SQL Injection]] e [[XSS (Cross-Site Scripting)|XSS]].

## Hands On (vídeos)
Os 2 principais tipos de ataque a servidores no mundo, **SQL/Command Injection** e **XSS**: como funcionam e como evitá-los. Segundo o resumo final, a aula também abordou **como o XSS pode impactar a autenticação JWT**, mas o texto do PDF não detalha isso.

## Ataques a servidores: 7 categorias
Quem tem um servidor na nuvem lida com algum ataque praticamente todos os dias.

| Categoria | Ataque | Como funciona |
|---|---|---|
| 1. **Injeção** | **SQL Injection** | Injeta comandos SQL maliciosos em campos de texto para acessar, modificar ou excluir dados do banco |
| | **Command Injection** | Injeta comandos do **sistema operacional** em campos de entrada para executá-los no servidor. É perigoso quando o código executa comandos de prompt ou shell |
| 2. **Negociação de sessão** | **Man-in-the-Middle (MITM)** | O atacante fica **entre** duas partes, interceptando ou manipulando o que elas trocam sem que saibam. O objetivo é obter senhas, cartões etc. |
| | **Sessão fixa** | Em sistemas com autenticação por sessão, o atacante fixa uma sessão válida e **força o usuário legítimo a adotá-la**, explorando falhas na geração de identificadores de sessão |
| 3. **Autenticação** | **Força bruta** | Uma série de tentativas para adivinhar login e senha |
| | **Senha fraca** | Como a força bruta, mas usando **senhas fracas ou comuns** na internet |
| 4. **Negação de serviço** | **DoS** | Sobrecarrega servidor ou rede com um número gigante de solicitações, deixando o serviço inacessível. Parte de **um único ponto** |
| | **DDoS** | O mesmo objetivo, mas usando uma **rede de computadores zumbis** que atacam de vários lugares |
| 5. **Protocolos e camadas de rede** | **Exploração de vulnerabilidades de rede** | Explora falhas em protocolos de rede para obter acesso não autorizado |
| | **Envenenamento de ARP** | O ARP associa IPs a endereços MAC em redes Ethernet. O ataque compromete essa tabela, redirecionando o tráfego para um servidor malicioso (interrupção ou interceptação de dados) |
| 6. **Aplicativos web no servidor** | **XSS** | Injeta scripts maliciosos em páginas web para acessar os **cookies** de usuários legítimos e, assim, obter acesso ao usuário |
| 7. **Escuta de rede** | **Sniffing de pacotes** | Monitora o tráfego para capturar dados confidenciais entre servidor e clientes (login, senha, cartões) |
| | **Interceptação de dados confidenciais** | Monitora a rede que o usuário acessa para interceptar dados **em trânsito** |

## Casos famosos
**SQL Injection: Sony PlayStation Network (2011)**
- **Tipo**: um app web da PSN não validava corretamente as entradas, e os atacantes inseriram comandos SQL nos campos de input, manipulando as consultas ao banco.
- **Resultado**: acesso a dados pessoais e financeiros de **milhões** de usuários (nomes, endereços, datas de nascimento, cartões de crédito).
- **Duração**: o ataque ocorreu em abril de 2011 e só foi detectado vários dias depois, em 19 de abril.
- **Consequências**: a Sony teve de tirar a PSN do ar, além da perda de reputação.

**XSS: MySpace (2005)**
- **Tipo**: Samy Kamkar achou uma falha que permitia injetar JavaScript em perfis. O script ficava no perfil dele, e quem o visitava recebia o script e virava amigo de Kamkar.
- **Resultado**: em horas, centenas de milhares de perfis afetados.
- **Consequência**: o MySpace desativou temporariamente o serviço para conter o ataque.

**Outros casos citados**

| Ataque | Caso |
|---|---|
| SQL Injection | Yahoo (2014): mais de 500 milhões de contas · Ashley Madison (2015) · TalkTalk (2015) · Equifax (2017, combinação de vulnerabilidades incluindo SQL Injection): mais de 143 milhões de pessoas · Uber (2016): mais de 50.000 motoristas |
| XSS | Sony Pictures (2014): e-mails, dados de funcionários, filmes não lançados · Twitter (2010): worm com mensagens automáticas · eBay (2014): redirecionamento para phishing · WhatsApp Web (2015): acesso a conversas · Yahoo Finance (2017): redirecionamento para sites maliciosos · BBC (2015): mensagens políticas e ofensivas no site |

> [!note] O título da aula cita **buffer overflow**, mas o texto do PDF não detalha esse ataque. Ele só aparece na aula 1, como algo que a validação e a sanitização de dados ajudam a evitar.

## Referências
Aiqon, *TOP 10 – Os mais comuns ciberataques* · CNET, *Sony PlayStation site victim of SQL-injection attack* · Innovation & Tech Today, *Samy Worm* · Simplilearn, *Types of Cyber Attacks* (2023)
