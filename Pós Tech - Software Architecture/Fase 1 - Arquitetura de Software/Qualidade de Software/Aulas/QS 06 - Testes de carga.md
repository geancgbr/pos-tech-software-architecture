---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 6
fonte: "Aula 06 - Testes de carga.pdf"
---

# QS 06 - Testes de carga

← [[QS 05 - Trabalhando com BDD]] · [[Qualidade de Software]]

> [!summary] Em uma frase
> O [[Teste de Carga e Teste de Estresse|teste de carga]] avalia o desempenho em **condições normais** de uso, e o de **estresse**, em **condições extremas**. As ferramentas da aula são o [[Ferramentas de Teste de Carga (JMeter e K6)|JMeter e o K6]].

## Hands On (vídeo)
Criação de testes de carga com **K6** e **JMeter**, que medem desempenho e escalabilidade e avaliam a aplicação em diferentes cenários de carga.

## Carga × estresse
Os dois são **testes de desempenho**. Têm semelhanças, mas diferem na **finalidade** e nos aspectos avaliados.

| | Teste de carga | Teste de estresse |
|---|---|---|
| Condição | **Uso normal**, com carga de trabalho típica | **Extrema**, além dos limites normais |
| Verifica | A capacidade de lidar com o **número esperado** de usuários e transações | A **capacidade máxima**, com carga excessiva e intensiva |
| Objetivo | Identificar **gargalos**, avaliar a **estabilidade** e atender aos requisitos de desempenho | Identificar os **pontos de falha**: recursos esgotados, tempo de resposta excessivo, comportamento inesperado |

**Benefícios do teste de carga**
- **Melhora do desempenho**: identifica gargalos e otimiza para cargas altas.
- **Garantia da resiliência**: avalia se o sistema mantém a estabilidade sob pressão.
- **Prevenção de falhas**: antecipa problemas de escalabilidade e capacidade.

## Ferramentas
As duas mais conhecidas na comunidade. Têm funcionalidades semelhantes, mas diferem em **arquitetura, recursos e usabilidade**.

| | JMeter | K6 |
|---|---|---|
| Tipo | Código aberto, desenvolvido em **Java** | Código aberto, para testes de carga e performance |
| Destaque | Simula **centenas ou milhares de usuários virtuais** executando ações num período | **Consumo mínimo de recursos**, alto desempenho, para alta carga (testes de **pico, estresse, absorção**) em pré-produção e controle de qualidade |
| Instalação | Baixar pelo link do GitHub, descompactar e abrir o executável do seu SO em `<instalação do JMeter>\bin\` | Windows: Chocolatey ou instalador · Linux: `sudo dnf install https://dl.k6.io/rpm/repo.rpm` e `sudo dnf install k6` · macOS: `brew install k6` |
| Pré-requisitos | Não citados | Noções de **JavaScript** e **Visual Studio Code** |

As Figuras 1 e 2 do PDF mostram o executável e a interface do JMeter.

**Primeiro teste com K6**: crie um `index.js`:

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export default function () {
  http.get('https://test.k6.io');
  sleep(1);
}
```

Depois rode `k6 run index.js`. O resultado esperado aparece na Figura 3 do PDF.

## Referências
Aniche, *Testes automatizados de software* (2015) · Apache, *Download Apache JMeter* (2023) · Chocolatey (2023)
