---
tags: [pos-tech/fase-1, qualidade, aula]
disciplina: Qualidade de Software
aula: 4
fonte: "Aula 04 - Testes de integração.pdf"
---

# QS 04 - Testes de integração

← [[QS 03 - Aplicando TDD na prática]] · [[Qualidade de Software]] · Próxima → [[QS 05 - Trabalhando com BDD]]

> [!summary] Em uma frase
> O [[Teste de Integração|teste de integração]] valida a **interação entre componentes ou módulos**: garante que partes testadas individualmente funcionem **em conjunto**, comunicando-se e trocando dados como esperado.

## Hands On (vídeo)
Os primeiros testes de integração na plataforma **.NET**: configurar o ambiente de teste, criar casos de teste de integração e executá-los.

## Por que são importantes
- Um sistema complexo tem várias partes independentes (módulos, serviços, componentes), cada uma testável por **testes unitários**. Mas testar cada parte isoladamente **não garante** que elas funcionem integradas.
- Os testes de integração verificam se as partes se comunicam, processam e trocam informações conforme o esperado.
- Identificam **incompatibilidades entre componentes**, **erros de comunicação** e **falhas na passagem de dados**, entre outros.
- São fundamentais para a eficiência, a confiabilidade e a estabilidade do sistema como um todo.

## Como fazer: 3 passos
1. **Configurar o ambiente**: controlado e **semelhante ao de produção**, com bancos de dados, serviços externos, APIs e outros recursos. Virtualização ou containers (como **Docker**) facilitam.
2. **Escrever os testes**: com **cenários realistas**, cobrindo comunicação entre módulos, passagem de dados entre serviços e interação com sistemas externos.
3. **Executar e analisar**: de forma **automatizada**, registrando os resultados e verificando se os componentes se comunicam corretamente.

## Estratégias
| Estratégia | Como funciona | Simulação ou observação |
|---|---|---|
| **Top-Down** | Começa pelos módulos **mais externos** e desce até os mais internos | Módulos externos simulados ou **stubs** |
| **Bottom-Up** | Começa pelos módulos **mais internos** (baixo nível) e sobe até os superiores | Dependências externas simuladas ou **mock objects** |
| **Sandwich** (híbrida) | Combina top-down e bottom-up: testa os módulos superiores e inferiores **ao mesmo tempo**, integrando de forma centralizada | O texto não cita |
| **Big Bang** | **Todos** os módulos integrados e testados de uma vez, **sem abordagem incremental** | Útil com **poucos módulos** ou módulos independentes entre si |
| **Integração contínua** | Integra e testa **continuamente**, à medida que novos módulos entram | Encontra problemas o mais cedo possível |

## Tipos de validação
| Validação | O que verifica |
|---|---|
| **Interface** | Se as interfaces entre componentes estão bem definidas e funcionando: parâmetros de entrada, retorno, comportamento |
| **Dados** | Transmissão e processamento corretos dos dados: formatos, transformações, integridade, tratamento de erros e exceções |
| **Fluxo de controle** | Chamadas de funções, sequência de operações, tratamento de eventos, transições entre estados |
| **Comportamento** | Se o comportamento **global** é consistente: cenários de uso, casos abrangentes, resultados esperados |
| **Desempenho** | Tempos de resposta, capacidade de carga, escalabilidade, eficiência |

## Quem faz
Não há um responsável específico:
- **Equipe de teste**: dedicada, especializada em estratégias, técnicas e ferramentas. Planeja, projeta e executa.
- **Especialistas em desenvolvimento**: testam à medida que implementam e integram, garantindo que seu código funcione com os outros módulos.
- **Equipe de qualidade (QA)**: em algumas organizações, faz a intermediação entre devs e equipe de teste, garantindo a integração e os critérios de qualidade.

O importante é que haja **colaboração** entre todos os envolvidos.

## Referência
Microsoft, *Testes de integração no ASP.NET Core* (2023)
