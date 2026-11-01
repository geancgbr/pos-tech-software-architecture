---
tags: [pos-tech/fase-3, monitoramento, datadog, dashboards, conceito]
aliases: [Timeboard, Timeboards, Screenboard, Screenboards]
---

# Dashboards do Datadog

Transformam métricas, traces e logs em **visualizações claras e acionáveis** ([[MAV 06 - Criando dashboards com DD]]).

| | Timeboard | Screenboard |
|---|---|---|
| Foco | **Análise temporal** | **Layout livre** |
| Tempo | Eixo **global e sincronizado** | Cada widget pode ter **seu intervalo** |
| Uso | Incidentes, pós-deploy, exploração | NOC, liderança, arquitetura, equipes |

- **Widgets**: Timeseries · Query Value · Top List · Table · Note/Free Text · Image · Geomap.
- **Variáveis de template** (`$env`, `$service`): dashboards reutilizáveis e interativos.
- **Outros**: compartilhamento (Screenboards com URL pública), permissões, Modo TV, exportar/importar JSON.
- Comparação: os dashboards do [[New Relic]] usam [[NRQL]] e variáveis `{{nome}}` ([[MAV 11 - Criando dashboards com New Relic]]).

Aparece em: [[MAV 06 - Criando dashboards com DD]]
