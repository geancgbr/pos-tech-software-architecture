---
tags: [pos-tech/fase-3, api-gateway, aula]
disciplina: API Gateway
aula: 1
fonte: "API Gateway/1 - Introdução ao APIGW_revFinal.pdf (Milton Camara)"
---

# APIGW 01 - Introdução ao API Gateway

[[API Gateway]] · Próxima → [[APIGW 02 - API Management do Azure]]

> [!summary] Em uma frase
> O **API Gateway** (API GW, ou só GW) é um **componente intermediário** que atua como **ponto de entrada para todas as chamadas de API**: um "guardião" que direciona as solicitações aos serviços e coordena as respostas. O caso real do autor: o **primeiro debate presidencial de 2022** numa emissora, em que o pico de acesso foi resolvido **apontando o GW** para APIs replicadas em muitos **Pods** no **[[Kubernetes]]**.

## Hands On (vídeo)
Implementar um **API Gateway simples com .NET Core 7**, que gerencia o acesso a duas ou mais APIs fictícias. Pré-requisitos: **.NET Core 7 SDK** e uma ferramenta como o **Postman**. No Saiba Mais, depois do caso do debate, o texto convida para a "aula em vídeo", com mais detalhes daquela arquitetura.

**1. As APIs fictícias** (`dotnet new webapi -n MyAPIs`), em `Controllers/WeatherForecastController.cs`:
```csharp
[ApiController]
[Route("[controller]")]
public class APIsController : ControllerBase
{
    [HttpGet("api1")]
    public IActionResult GetAPI1() { return Ok(new {message = "Resposta da API 1"}); }

    [HttpGet("api2")]
    public IActionResult GetAPI2() { return Ok(new {message = "Resposta da API 2"}); }
}
```

**2. O gateway** (`dotnet new webapi -n APIGateway` e `dotnet add package System.Net.Http`):
```csharp
[ApiController]
[Route("[controller]")]
public class GatewayController : ControllerBase
{
    private readonly HttpClient _client;

    public GatewayController()
    {
        _client = new HttpClient { BaseAddress = new Uri("http://localhost:5000") };
    }

    [HttpGet("api1")]
    public async Task<IActionResult> GetAPI1()
    {
        var response = await _client.GetAsync("/apis/api1");
        var content = await response.Content.ReadAsStringAsync();
        return Ok(content);
    }
    // GetAPI2 igual, chamando "/apis/api2"
}
```

**3. Testando**: `dotnet run` nas APIs; em outro terminal, `dotnet run --urls http://localhost:5001` no gateway; no Postman, GET em `http://localhost:5001/gateway/api1` e `/gateway/api2`.

- É uma implementação **básica**. Em cenários reais, o gateway seria muito mais complexo: **autenticação, limitação de requests, balanceamento de carga** e muito mais.

> [!note] A indentação do código foi refeita e o `GetAPI2` do gateway foi resumido num comentário; o PDF traz o método completo, idêntico ao `GetAPI1` com `/apis/api2`.

## O que é
- Com a demanda por software **escalável e interconectado**, as **APIs** ganham importância: permitem que aplicativos compartilhem dados e funcionalidades. Mas **gerenciar várias APIs** e garantir segurança e desempenho é um desafio.
- O API Gateway é o **componente intermediário** e **ponto de entrada** de todas as chamadas: um **"guardião"** que direciona as solicitações e coordena as respostas. Em essência, **um único ponto de contato** para várias APIs.
- **Figura 1**: o gateway no centro, integrado a serviços de **segurança, autenticação, monitoramento** etc. Assim, o desenvolvimento foca no projeto com alguns pontos básicos de segurança, e o GW cuida de outras camadas, como **segurança** e **cache com rate limit**.
- **Figura 2** (Microsoft): o GW integrado a microsserviços. O request HTTP começa com o usuário, passa por **autenticação no Azure AD** e, autenticado, consome os dados do **Backend**.

## Benefícios (os motivadores do autor)
| Benefício | O que o PDF diz |
|---|---|
| **Consolidação e simplificação** | Várias APIs num **único ponto de acesso** |
| **Segurança** | Local **centralizado** para políticas de segurança, autenticação e autorização, de forma consistente |
| **Monitoramento e análise** | Métricas de desempenho, tempos de resposta, erros e insights |
| **Transformação de dados** | Adaptar entradas e saídas a diferentes formatos ou simplificar as solicitações |
| **Cache** | Melhorar o desempenho, reduzir a carga nos serviços e acelerar as respostas para solicitações frequentes |

## O caso do debate presidencial (2022)
- O autor era **Techlead** numa emissora e precisava garantir o **primeiro debate presidencial**, transmitido em parceria com o **Google** (Figura 3, com pontos alterados por privacidade).
- De "x" usuários, num curto período, o número foi a **"X elevado a 1000"**, e os servidores não estavam preparados para o pico. Como resolver **sem republicar o site** nem derrubar os usuários, principalmente os do **aplicativo mobile**, e sem replicar o aplicativo?
- **Solução**: como **tudo apontava para o GW**, fizeram outros apontamentos para uma estrutura com **Kubernetes**, replicando as APIs em muitos **[[Pod|PODs]]**. Isso só foi possível porque tudo estava **centralizado no GW**.

## Referências
Atatus (2022) · Bryant (2018) · Mahadevan (2019) · Microsoft: Integração empresarial básica no Azure · Shah (2020)
