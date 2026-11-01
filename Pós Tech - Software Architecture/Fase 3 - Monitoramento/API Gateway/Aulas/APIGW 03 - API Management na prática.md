---
tags: [pos-tech/fase-3, api-gateway, azure, aula]
disciplina: API Gateway
aula: 3
fonte: "API Gateway/3 - APIM na Prática_revFinal.pdf (Milton Camara)"
---

# APIGW 03 - API Management na prática

← [[APIGW 02 - API Management do Azure]] · [[API Gateway]] · Próxima → [[APIGW 04 - Conhecendo o Kong]]

> [!summary] Em uma frase
> O **[[Azure API Management (APIM)]]** na prática, numa **série de vídeos**: criar uma **API manual**, importar por **OpenAPI**, aplicar **[[Políticas de API]]** (como "Verificar chave de consulta ou cabeçalho") e políticas de segurança (como a "Chave de assinatura"), **monitorar** (tráfego, tempo de resposta, erros, latência), usar **cache** e o **Portal do Desenvolvedor**.

## Hands On (vídeos)
**Configuração**: portal.azure.com → **"+ Criar um recurso"** → **"API Management"** → **"Criar"** → assinatura, grupo de recursos, **nome exclusivo**, localização → **"Revisar + criar"** → **"Criar"**.

| Passo | Como |
|---|---|
| **API manual** | No APIM, **"APIs"** → **"+ Adicionar API"** → **"API em branco"**: nome e **Web Service URL** (ex.: um serviço de teste) → **"Criar"** |
| **Segurança** | Na página de design, **"Configurações"** → **"Políticas de Segurança"** → **"Chave de assinatura"**, para exigir uma chave de API |
| **Políticas** | **"Design"** → **"Políticas de entrada"** → **"+ Adicionar política"** → **"Verificar chave de consulta ou cabeçalho"** |
| **Monitoramento** | **"Monitoramento"**: métricas como **"Tráfego da API"** e **"Tempo de Resposta"**. **"Alertas"** → **"+ Novo alerta"** |
| **Cache** | **"Cache"** → **"+ Adicionar"** e o assistente |
| **Portal do Desenvolvedor** | Como as APIs aparecem para devs externos; selecionar a API, um método e **"Testar"** |

- O Azure pode atualizar a interface; consultar sempre a **documentação oficial**.

## Funcionalidades do APIM
**Gerenciamento centralizado** (criação, publicação, **versionamento** e **desativação**) · **controle de acesso** (autenticação e autorização) · **políticas de API** (segurança, transformação, controle de tráfego) · **monitoramento e análise** · **Portal do Desenvolvedor** · **cache e performance**.

## Criando uma API manual
Acessar o painel → criar uma nova API → definir **nome, descrição e endpoint** → políticas de segurança (ex.: **autenticação por chave de API**) → políticas de transformação, se necessário → **publicar** e obter a **URL pública**.

## OpenAPI
O APIM permite **importar APIs existentes** por especificações **OpenAPI** (antes conhecidas como **Swagger**).

> [!note] O texto diz "veremos como trabalhar com **OpenAI**" e, na mesma frase, explica a importação por **OpenAPI**. Está assim no PDF.

## Políticas de API
Ver [[Políticas de API]].
- São **conjuntos de regras e ações** aplicadas a uma API específica. Atuam como **intermediárias** entre as solicitações e as respostas, controlando como os dados são **tratados, transformados e protegidos**.
- **Segurança** (uma das áreas mais cruciais): exigir **chaves de API**, **tokens de acesso** ou **OAuth**.
- **Experiência dos devs**: consumir com confiança, **reduzindo a curva de aprendizado** e facilitando a integração.

## Monitoramento
- Não é só **reativo**: é também **preventivo**. Acompanhar tráfego, desempenho e uso identifica problemas **antes** de virarem interrupções e orienta otimização, escalabilidade e planejamento.

| Métrica | Para quê |
|---|---|
| **Tráfego da API** | Picos e tendências sazonais; **escalonamento proativo** |
| **Tempo de Resposta** | Gargalos e otimização |
| **Taxas de Erro** | Estabilidade (com as taxas de sucesso) |
| **Latência** | Pontos problemáticos |
| **Taxas de Uso por Recurso** | Onde focar a otimização |

## Cache
- O desempenho é **crítico** para a satisfação; latência e tempo de resposta podem levar à **frustração** e ao **abandono** da aplicação.
- **Cache**: armazenamento **temporário** de dados acessados com frequência, para reduzir a sobrecarga no backend. No APIM, aplica-se às **respostas das APIs**. Ver também [[Estratégias de Cache]].
- **Benefícios**: melhoria do desempenho · redução da latência ("respostas quase instantâneas") · economia de recursos · escalabilidade.

## Portal do Desenvolvedor
Componente essencial do APIM: interface amigável para os devs e, segundo o PDF, com papel crucial na implementação de **cache, monitoramento e políticas de API**.

## Referências
Lee (2022): Azure APIM: more than just a Gateway · Microsoft: O que é o Gerenciamento de API do Azure? · Suryawanshi (2022)
