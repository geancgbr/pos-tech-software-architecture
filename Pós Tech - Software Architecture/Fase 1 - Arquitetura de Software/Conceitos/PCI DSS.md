---
tags: [pos-tech/fase-1, seguranca, conceito]
aliases: [PCI, Payment Card Industry Data Security Standard]
---

# PCI DSS

**Padrão de Segurança de Dados para a Indústria de Cartões de Pagamento.**

- **Aula 1**: conjunto de requisitos para proteger os dados do processamento de cartão de crédito. Iniciativa do **PCI SSC** (Payment Card Industry Security Standards Council), uma organização global de empresas de cartões de pagamento, como Visa, MasterCard, American Express, Discover e JCB.
- **Aula 6**: surgiu quando as principais bandeiras se uniram para proteger os titulares de cartão, diante da demanda por meios eletrônicos (cartão, PIX).

**Pontos principais** (aula 6)
- Rede segura: firewalls, **sem senhas padrão**.
- Proteger os dados dos titulares: **criptografar**; **mascarar (truncar)** o número do cartão.
- Política de segurança de informações para funcionários e contratados.
- Controle de acesso: **[[Princípio do Menor Privilégio|acesso mínimo necessário]]**; identificação única.
- Monitorar e testar as redes regularmente.
- Política de segurança de sistemas: antimalware, antivírus atualizado.
- Controles de segurança no desenvolvimento de aplicações.
- Número de identificação único para cada pessoa com acesso.

A conformidade é **obrigação regulatória** e também demonstração de compromisso com a segurança, que gera reputação de confiança. É um dos padrões verificados pelo **AWS Security Hub**.

Aparece em: [[DS 01 - Vulnerabilidades, ataques e intrusões]], [[DS 06 - Padrões de segurança]]
