---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [Ataques a servidores, Ataques, MITM, Man-in-the-Middle, DoS, DDoS, Força bruta, Sessão fixa, Envenenamento de ARP, Sniffing]
---

# Tipos de Ataques

Os principais ataques a servidores, nas 7 categorias da aula 2:

| Categoria | Ataques |
|---|---|
| **Injeção** | [[SQL Injection e Command Injection\|SQL Injection, Command Injection]] |
| **Negociação de sessão** | **Man-in-the-Middle** (intercepta ou manipula a comunicação entre duas partes) · **Sessão fixa** (força o usuário a adotar uma sessão fixada pelo atacante) |
| **Autenticação** | **Força bruta** (várias tentativas de login e senha) · **Senha fraca** (tenta senhas fracas e comuns) |
| **Negação de serviço** | **DoS** (sobrecarga a partir de um único ponto) · **DDoS** (rede de computadores zumbis, de vários lugares) |
| **Protocolos e camadas de rede** | **Exploração de vulnerabilidades de rede** · **Envenenamento de ARP** (corrompe a tabela IP↔MAC e redireciona o tráfego) |
| **Aplicativos web no servidor** | [[XSS (Cross-Site Scripting)\|XSS]] (scripts maliciosos para pegar cookies) |
| **Escuta de rede** | **Sniffing de pacotes** (captura dados no tráfego) · **Interceptação de dados confidenciais** (dados em trânsito) |

Segundo a aula 2, os ataques mais comuns e evitáveis incluem DDoS, SQL Injection, Command Injection e XSS. A descrição completa de cada um está em [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]].

Aparece em: [[DS 02 - Buffer overflows, cross-site scripting e SQL injection]]
