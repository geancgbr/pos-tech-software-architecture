---
tags: [pos-tech/fase-4, resiliencia, microsservicos, aula]
disciplina: Resiliência em Microsserviços
aula: 3
fonte: "Resiliência em microservices/Aula 03 - Resiliencia na prática.pdf"
---

# RES 03 - Resiliência na prática

← [[RES 02 - Padrões de resiliência]] · [[Resiliência em Microsserviços]] · Próxima → [[RES 04 - Service Mesh e controle de tráfego]]

> [!summary] Em uma frase
> Resiliência **não é eliminar falhas, mas reduzir seus impactos**. A aula implementa à mão **Idempotência** (Python), **Timeout** (Go) e **Retry com backoff exponencial e jitter** (Node.js) e depois passa ao **Resilience4j** em Java: **janelas deslizantes** do Circuit Breaker (contagem e tempo, **Subtract-on-Evict**), parâmetros, **fallback** e boas práticas.

## Hands On (vídeos)
Nas videoaulas: os padrões **Retry, Bulkhead e Rate Limiter** com a biblioteca **Resilience4j** em projetos Java, com dicas de configuração, boas práticas e uso da documentação oficial.

## Idempotência na prática
**Exemplo real**: num serviço de pagamento, se o cliente clicar duas vezes em "Pagar" ou um retry reenviar após um timeout, deve haver **uma única cobrança**: o sistema reconhece a operação já processada e **retorna o resultado anterior**. Ver [[Idempotência]].

Três etapas:
1. **Gerar uma chave única** (**Idempotency Key**), **geralmente** criada pelo cliente (por exemplo, um **UUID**) e enviada **no cabeçalho**.
2. O servidor **armazena** o par `idempotency_key` + resposta num repositório **persistente** (banco ou cache distribuído).
3. Numa nova chamada com a mesma chave, **retorna a resposta armazenada**, sem executar de novo.

Código-fonte 1 (Python, Flask + SQLite), endpoint `/process-payment`:
```python
from flask import Flask, request, jsonify
import sqlite3
import uuid

app = Flask(__name__)

# Inicializa o banco de dados para armazenar requisições
def init_db():
    conn = sqlite3.connect("idempotency.db")
    cursor = conn.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS requests (
            idempotency_key TEXT PRIMARY KEY,
            response TEXT
        )
    """)
    conn.commit()
    conn.close()

init_db()

@app.route("/process-payment", methods=["POST"])
def process_payment():
    # Obtém a chave de idempotência do cabeçalho
    idempotency_key = request.headers.get("Idempotency-Key")
    if not idempotency_key:
        return jsonify({"error": "Idempotency-Key is required"}), 400

    conn = sqlite3.connect("idempotency.db")
    cursor = conn.cursor()

    # Verifica se a operação já foi processada
    cursor.execute("SELECT response FROM requests WHERE idempotency_key = ?",
                   (idempotency_key,))
    row = cursor.fetchone()
    if row:
        conn.close()
        return jsonify({"status": "already_processed", "result": row[0]})

    # Simula processamento de pagamento
    payment_id = str(uuid.uuid4())
    response = {"status": "success", "payment_id": payment_id}

    # Salva a resposta para futuras repetições
    cursor.execute("INSERT INTO requests (idempotency_key, response) VALUES (?, ?)",
                   (idempotency_key, str(response)))
    conn.commit()
    conn.close()
    return jsonify(response)

if __name__ == "__main__":
    app.run(debug=True)
```

> [!note] A extração do PDF perdeu a indentação dos códigos desta aula; ela foi refeita na nota.

- Chave já existente → mesmo resultado da operação anterior; chave nova → processa e registra. Ver a figura sem número "Idempotency in Scalable Distributed System" (Amplification).
- **Recomendações**: definir um **tempo de expiração** para as chaves (ex.: **24 horas**) e usar um **banco transacional confiável** para prevenir **condições de corrida** com múltiplas instâncias.

## Timeout na prática
- Sem timeout, um atraso num serviço **pode** se propagar e afetar toda a aplicação. **Exemplo**: o serviço de pagamentos chama um gateway externo lento; com timeout, a operação é **cancelada** e o sistema retorna erro ou aciona **fallback**. Ver [[Timeout]].

Código-fonte 2 (Go):
```go
package main

import (
    "context"
    "encoding/json"
    "log"
    "net/http"
    "time"
)

type PaymentResponse struct {
    Status    string `json:"status"`
    PaymentID string `json:"payment_id,omitempty"`
    Error     string `json:"error,omitempty"`
}

func processPaymentHandler(w http.ResponseWriter, r *http.Request) {
    ctx, cancel := context.WithTimeout(r.Context(), 2*time.Second) // Timeout de 2 segundos
    defer cancel()

    resultChan := make(chan PaymentResponse, 1)

    // Simula chamada externa com timeout
    go func() {
        time.Sleep(3 * time.Second) // serviço externo demorando
        resultChan <- PaymentResponse{Status: "success", PaymentID: "12345"}
    }()

    select {
    case <-ctx.Done():
        // Timeout atingido
        w.WriteHeader(http.StatusGatewayTimeout)
        json.NewEncoder(w).Encode(PaymentResponse{
            Status: "failed",
            Error:  "operation timed out",
        })
    case res := <-resultChan:
        // Sucesso
        w.WriteHeader(http.StatusOK)
        json.NewEncoder(w).Encode(res)
    }
}

func main() {
    http.HandleFunc("/process-payment", processPaymentHandler)
    log.Println("Servidor iniciado em :8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```
- `context.WithTimeout` limita a operação a **2 s**; sem resposta a tempo, o sistema devolve **504 Gateway Timeout**.
- **Dicas**: ajustar o timeout ao tempo de resposta **esperado de cada serviço**; **sempre** chamar `defer cancel()` para não vazar contexto; em algo crítico, ter um **fallback**.

## Retry com backoff exponencial na prática
- Repetir **imediatamente** **pode** piorar o problema, aumentando a carga num serviço debilitado. Com **backoff exponencial**, cada tentativa espera mais, **geralmente dobrando** o intervalo. Ver [[Retry e Backoff Exponencial]].

Código-fonte 3 (Node.js):
```javascript
const crypto = require('crypto');

// Função simulando chamada a serviço externo
async function callExternalService() {
  // Simula falha em 70% das tentativas
  if (Math.random() < 0.7) {
    throw new Error("Falha temporária no serviço externo");
  }
  return "Operação bem-sucedida";
}

async function retryWithBackoff(maxRetries, baseDelay) {
  for (let attempt = 1; attempt <= maxRetries; attempt++) {
    try {
      const result = await callExternalService();
      console.log(`✅ Operação bem-sucedida na tentativa ${attempt}`);
      return result;
    } catch (err) {
      if (attempt === maxRetries) {
        throw new Error(`❌ Operação falhou após ${maxRetries} tentativas: ${err.message}`);
      }
      // Calcula tempo de espera com backoff exponencial e jitter
      const sleep = baseDelay * Math.pow(2, attempt - 1);
      const jitter = crypto.randomInt(0, Math.floor(sleep / 2)); // aleatoriedade
      const waitTime = sleep + jitter;
      console.warn(`Falha na tentativa ${attempt}: ${err.message}. Repetindo em ${waitTime}ms...`);
      await new Promise((resolve) => setTimeout(resolve, waitTime));
    }
  }
}

// Executa o retry
(async () => {
  try {
    const result = await retryWithBackoff(5, 500); // 5 tentativas, 500ms base
    console.log(result);
  } catch (err) {
    console.error(err.message);
  }
})();
```

> [!note] Na extração, a mensagem do `console.warn` saiu quebrada em duas linhas fora de ordem; a linha foi remontada.

- Até **5 tentativas**; a espera **dobra** a cada falha (500 ms → 1 s → 2 s → 4 s...) e um **jitter** evita que vários clientes **reiniciem as tentativas de forma sincronizada**. Se todas falharem, retorna erro.

## Resilience4j
- Biblioteca Java para resiliência de forma **simples e declarativa**. A ideia **não é exclusiva do Java**: **Go** (Go-resiliency, Resilience), **Node.js** (opossum para circuit breaker, p-retry), **.NET** (Polly). Ver [[Resilience4j]].
- Criado por **Robert Winkler** como alternativa **moderna, leve e modular** ao **Netflix Hystrix**, descontinuado em **2018**. O Hystrix era ligado à arquitetura baseada em **threads** e ao modelo do Spring Boot; o Resilience4j aproveita o **Java 8+** (**Lambdas, Optional**).
- **Por que foi criado**: usar **só os módulos necessários** (Circuit Breaker, Retry, Bulkhead) sem dependências desnecessárias; funciona com **Spring Boot**, mas também de forma **independente**.

## Circuit Breaker e janelas deslizantes
- O objetivo é evitar **falhas em cascata**, deixando o sistema **degradar graciosamente** (Figura 1). Ver [[Circuit Breaker]].
- Usa uma **janela deslizante** para agregar os resultados das chamadas, **por contagem ou por tempo**:

| Janela | Como funciona |
|---|---|
| **Por contagem** | Um número fixo de medições num **array circular** (ex.: tamanho 10 = últimas 10 chamadas). A cada chamada, a soma é atualizada somando o novo valor e subtraindo o mais antigo: **Subtract-on-Evict**. Resumo em **O(1)**; memória **O(n)**, proporcional ao tamanho da janela |
| **Por tempo** | **Buckets** com agregações parciais num array circular (ex.: janela de 10 s = **10 buckets**, um por segundo). O bucket do segundo atual é atualizado; ao descartar o mais antigo, sua agregação é subtraída (também **Subtract-on-Evict**). Cada bucket guarda só agregações: chamadas com **falha**, **lentas**, o **total** e a **soma da duração** |

- Dependência Maven (Código-fonte 1 da segunda parte):
```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-circuitbreaker</artifactId>
    <version>2.0.2</version>
</dependency>
```

### Configuração por contagem e por tempo
- As configurações do `application.yml` estão **só em imagem**: ver as Figuras 2 (contagem) e 3 (tempo) do PDF.
- O código Java (Códigos-fonte 2 e 4) usa `@CircuitBreaker(name = "countBasedCircuitBreaker", fallbackMethod = "fallback")` (e `timeBasedCircuitBreaker`) num `@Service` cujo `processRequest()` lança `RuntimeException` quando `Math.random() > 0.5`; o método `fallback(Throwable throwable)` retorna `"Fallback ativado devido a: " + throwable.getMessage()`.

| Parâmetro | Por contagem | Por tempo |
|---|---|---|
| `slidingWindowType` | `COUNT_BASED`: número fixo de chamadas | `TIME_BASED`: chamadas num intervalo de tempo |
| `slidingWindowSize` | Quantas chamadas (ex.: **10** = últimas 10) | Duração em segundos (ex.: **10s**) |
| `failureRateThreshold` | % de falhas que abre o circuito (ex.: **50.0** = metade) | Idem, nos últimos 10 s |
| `waitDurationInOpenState` | Tempo **aberto** antes de ir a meio-aberto (ex.: **5s**) | Idem (ex.: **5s**) |

- A janela por tempo é "ideal" para analisar o comportamento de um serviço **ao longo de um período**.

> [!note] Nos parâmetros, o circuito abre quando a porcentagem de falhas é "**atingida**"; em "Como funciona", quando ela "**excede**" ou "**ultrapassa**" o limite.

> [!warning] Inconsistências do PDF
> - Na seção da janela **por tempo**, o texto repete "configuramos um Circuit Breaker com janela deslizante baseada em **contagem**".
> - A numeração recomeça e pula: Códigos-fonte 1 a 3 (Python, Go, Node.js), depois 1 (Maven), 2 e **4** (Java); não há Código-fonte 3 na segunda parte.
> - A figura "Idempotency in Scalable Distributed System" não tem número e vem antes da "Figura 1 – Circuit Breaker".

## Métodos de fallback
- Estratégia de **contingência**, chamada **automaticamente** quando o circuito está **aberto** ou uma **exceção** é lançada. Permite: retornar uma **resposta padrão**; executar um **caminho alternativo**; **logar** a falha e alertar os administradores. Ver [[Fallback e Graceful Degradation]].
- `fallbackMethod` define o método; ele recebe **a exceção capturada ou nenhum parâmetro**, conforme a lógica.
- Estados: **fechado** (chamadas normais e monitoradas) · **aberto** (bloqueadas; falhas registradas) · **meio-aberto** (após o tempo configurado, **uma chamada** é permitida para testar; com sucesso, volta a **fechado**).

> [!note] Aqui o meio-aberto permite "uma chamada"; na aula 2, "algumas requisições", e na aula 4, "uma quantidade limitada".

## Boas práticas
- **Limiares realistas**: usar dados históricos ou testes de performance para ajustar `failureRateThreshold` e `slowCallRateThreshold`, nem disparando à toa nem permissivo demais.
- **Combinar com Bulkhead**: protege threads e conexões, mesmo com o circuito "fechado". Ver [[Bulkhead]].
- **Fallbacks úteis**: mensagens claras ou ações alternativas (serviços de backup, valores padrão).
- **Monitorar** em tempo real: chamadas bem-sucedidas, com falha e lentas.

## O que vem por aí
**Service Mesh e Controle de tráfego**.

## Referências
JSession4D: Resilience4j com Spring Boot · Lydtech Consulting: Resilience4j overview · NashTech: Bulkhead no Resilience4j · Reflectoring: Rate limiting com Spring Boot e Resilience4j · Resilience4j: CircuitBreaker documentation
