---
tags: [pos-tech/fase-2, opentelemetry, observabilidade, conceito]
aliases: [Logging estruturado, Log estruturado, LogRecord, Logs]
---

# Logs Estruturados

**Logs não estruturados** (texto livre) são legíveis para humanos, mas **terríveis para máquinas**: buscar exige **regex**, lento, frágil e caro. **Logs estruturados** são escritos num formato de máquina, como **JSON**.

**Vantagens**: **pesquisa eficiente** por campos (`user_id="123"`, `duration_ms > 100`) · **análise de dados** (gerar métricas e visualizações) · **consistência** entre serviços. O OpenTelemetry **formaliza o logging estruturado como padrão**.

**O LogRecord do OTel**: **Timestamp** · **ObservedTimestamp** (recebido pelo coletor; a diferença pode indicar latência no pipeline) · **SeverityText** (INFO, WARN, ERROR) · **SeverityNumber** (INFO=9, ERROR=17) · **Body** · **Attributes** · **Resource attributes** (quem produziu, como `service.name`, `k8s.pod.name`) · **TraceId e SpanId**.

**TraceId e SpanId**: o campo **mais importante para a correlação**. Com eles, é possível ir do trace aos logs do span, do log de erro ao trace completo, e, de um pico de métrica, usar o **intervalo de tempo** para filtrar os logs com `level="ERROR"` e daí analisar os traces ([[Três Pilares da Observabilidade (Logs, Métricas e Traces)]]).

**Papel dos logs**: contexto detalhado (o "porquê" de um span lento), **eventos inesperados** e **auditoria e segurança**.

Aparece em: [[OTEL 01 - Introdução ao OpenTelemetry]], [[OTEL 04 - OpenTelemetry Logs (Loki)]]
