---
tags: [pos-tech/fase-2, docker, conceito]
aliases: [Container, Containers, Contêineres, Contêiner Docker]
---

# Contêiner

Um **ambiente isolado**, parecido com o de uma VM, onde roda uma aplicação. **Vários contêineres com aplicações diferentes rodam em paralelo no mesmo servidor**, e se um quebra (ex.: usa 100% da CPU), os outros não são afetados (aula 1).

- O isolamento vem dos **Namespaces**, e os limites de recursos, dos **Cgroups**: [[Cgroups e Namespaces]].
- **Analogia do navio cargueiro**: se um contêiner cai no mar, os outros e o navio (o **host**) não são afetados.
- **VMs × contêineres**: segundo a apostila, as diferenças "são poucas, mas mudam completamente o modo de execução e isolamento". As comparações estão nas Figuras 3 e 4 da aula 1, e o texto não as detalha.
- **Aula 6 (ECS)**: contêineres são **unidades leves e portáteis** que executam a aplicação de forma consistente, **independentemente do ambiente**.

**Gerenciamento** (aula 2): `docker container ls -a` · limitar recursos na criação com `--cpus=1` e `-m 512m` · conferir com `inspect` + `grep` · alterar em execução com **`update`**, sem derrubar o contêiner. Detalhes em [[DK 02 - Gerenciamento de contêineres]].

## Na disciplina GitHub Actions (aula 4)
- Pacote **leve e independente** com tudo de que o app precisa. É a **instância executável de uma imagem**: "a imagem em tempo de execução".
- Os contêineres **compartilham o kernel do SO**, mas mantêm processos e arquivos separados. Muitos rodam numa máquina, **sem o overhead de uma VM completa**.
- Podem ser iniciados, parados, movidos ou excluídos pela **API ou pela CLI** do Docker. → [[GHA 04 - Conceitos básicos de Docker]]

## Na disciplina Kubernetes (parte 1, aula 1)
| | Virtualização (VMs) | Contêineres |
|---|---|---|
| Cria | Uma "pequena máquina" completa (**hardware e SO**) | Uma "pequena máquina" na **camada do SO** da hospedeira |
| Compartilha | Só o **hardware** | O **hardware e o SO** |
| Peso | — (o PDF só compara) | **Muito mais leve e barata** do que uma VM |

São **semelhantes, não iguais**. No Kubernetes, um ou mais contêineres formam um [[Pod]]. → [[K8S1 01 - Introdução ao Kubernetes]]

Aparece em: [[DK 01 - Introdução ao Docker]], [[DK 02 - Gerenciamento de contêineres]], [[DK 06 - ECS]], [[K8S1 01 - Introdução ao Kubernetes]]
