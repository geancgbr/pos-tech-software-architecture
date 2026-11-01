---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 1
aula: 7
fonte: "Kubernetes/Aula 7.pdf (Thiago Adriano)"
---

# K8S1 07 - Probes

← [[K8S1 06 - Volumes]] · [[Kubernetes]] · Próxima → [[K8S1 08 - HPA (Horizontal Pod Autoscaler)]]

> [!summary] Em uma frase
> As **[[Probes do Kubernetes|probes]]** verificam a **saúde de um aplicativo** num Pod. Há três tipos: **Liveness** (está rodando? se não, reinicia o Pod), **Readiness** (está pronto para receber solicitações? se não, sai do balanceador de carga) e **Startup** (está iniciando corretamente? se não, reinicia o Pod).

## Hands On
Como configurar as probes Liveness, Readiness e Startup e testar o comportamento do Kubernetes em diferentes cenários.

## O que são
- Recursos para garantir a **confiabilidade** dos aplicativos no cluster. Verificam a **saúde** de um aplicativo em execução num Pod, garantindo que ele responda corretamente às solicitações.
- São definidas no **manifesto do Pod** (um arquivo YAML que descreve como o aplicativo deve ser implantado e executado). A configuração inclui **o tipo de probe, o caminho de solicitação e os intervalos de verificação**.
- **Por que usar**: mantêm o aplicativo saudável e pronto para receber solicitações, o que é especialmente importante em produção. **Sem as probes, os aplicativos podem falhar silenciosamente**, sem ninguém perceber, levando a interrupções e afetando a experiência do usuário.

## Os três tipos
| Probe | O que verifica | Se falhar |
|---|---|---|
| **Liveness** | Se o aplicativo está **em execução** e respondendo corretamente | O Kubernetes **reinicia o Pod** |
| **Readiness** | Se o aplicativo está **pronto para receber solicitações** | O Kubernetes **remove o aplicativo do balanceador de carga** |
| **Startup** | Se o aplicativo está **sendo iniciado corretamente** (inicializado e configurado) | O Kubernetes **reinicia o Pod** |

- **Por padrão**, as três usam um **endpoint HTTP**: é enviada uma solicitação **HTTP GET** ao endpoint especificado, esperando **200 OK**. Na Liveness, o PDF diz que quem envia a solicitação é o **kubelet**.
- **Liveness**: não se limita a HTTP. Também há probes **TCP** e **Exec**. Exemplo: uma Liveness do tipo TCP verifica se o aplicativo está rodando e **ouvindo numa porta específica**.
- **Readiness**: mesmo **em execução**, o aplicativo pode **ainda não estar pronto**. Exemplo: precisa de tempo para carregar dados ou inicializar uma conexão com um banco de dados. É especialmente importante em aplicativos que demoram para iniciar ou carregar dados.
- **Startup**: importante em aplicativos que demoram para **inicializar e configurar**. Os intervalos podem ser ajustados para verificar com mais ou menos frequência, conforme a **carga e a importância** do aplicativo.

## Boas práticas
- Usar **as três probes** (Liveness, Readiness e Startup).
- **Configurar os intervalos de verificação** conforme o aplicativo e o ambiente.
- Usar **endpoints diferentes para cada tipo de probe**, para evitar conflitos.
- Usar as **configurações padrão** do Kubernetes sempre que possível.
- Usar **com cuidado** as configurações avançadas (atrasos de inicialização, intervalos personalizados), para evitar efeitos colaterais.
- **Testar** as probes regularmente.
- Usar ferramentas de monitoramento, como o **Prometheus**, para monitorar as probes e o desempenho.
- **Documentar** as configurações no manifesto do Pod ou num arquivo de configuração.
- **Monitorar as falhas de probe**.

## Exemplo (Figura 1 do PDF)
Um Pod com o contêiner **"exemplo-container"** (imagem **"exemplo:latest"**), expondo a **porta 80** e usando as três probes:

| Probe | Atraso inicial | Intervalo | Tempo de espera máximo |
|---|---|---|---|
| **Liveness** | não citado no texto | **10 s** | **5 s** |
| **Readiness** | não citado no texto | **5 s** | **3 s** |
| **Startup** | **120 s** | **30 s** | **10 s** |

## Referência
Bass, Clements e Kazman, *Software Architecture in Practice* (2012)
