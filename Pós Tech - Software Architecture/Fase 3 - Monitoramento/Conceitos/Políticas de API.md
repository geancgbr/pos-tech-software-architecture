---
tags: [pos-tech/fase-3, api-gateway, azure, conceito]
aliases: [Política de API, API policies]
---

# Políticas de API

Segundo a aula 3, **conjuntos de regras e ações** aplicadas a uma API específica. Atuam como **intermediárias** entre as solicitações dos clientes e as respostas dos servidores, controlando como os dados são **tratados, transformados e protegidos** ([[APIGW 03 - API Management na prática]]).

- **Segurança**: autenticação e autorização robustas, exigindo **chaves de API**, **tokens de acesso** ou **OAuth**.
- **Experiência dos devs**: consumo com confiança, menor curva de aprendizado e integração mais fácil.
- **No APIM**: **"Políticas de entrada"** → "+ Adicionar política" → "Verificar chave de consulta ou cabeçalho"; em "Políticas de Segurança", a **"Chave de assinatura"**.
- Também aparecem como recurso do APIM: segurança, autenticação, autorização, **limitação de taxa** e transformações ([[APIGW 02 - API Management do Azure]]).

Aparece em: [[APIGW 02 - API Management do Azure]], [[APIGW 03 - API Management na prática]]
