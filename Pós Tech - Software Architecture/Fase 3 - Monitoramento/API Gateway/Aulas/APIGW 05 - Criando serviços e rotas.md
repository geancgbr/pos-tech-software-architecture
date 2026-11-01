---
tags: [pos-tech/fase-3, api-gateway, kong, aula]
disciplina: API Gateway
aula: 5
fonte: "API Gateway/POSTECH - Aula5_revFinal.pdf (Douglas Lima da Silva Martins)"
---

# APIGW 05 - Criando serviços e rotas

← [[APIGW 04 - Conhecendo o Kong]] · [[API Gateway]] · Próxima → [[APIGW 06 - Consumers]]

> [!summary] Em uma frase
> Colocar no ar o **King for Kong**, outra GUI para o **[[Kong]]**: clonar o repositório, criar um **Dockerfile**, fazer o **build** e rodar o container. O King gera um **mapa de dependências baseado em Consumers**, mas, por ser **client side** e sem login, o **Konga** acaba sendo superior. Ver [[Konga e King]].

> [!note] O título do PDF é "Criando serviços e rotas", mas o conteúdo é o King. O texto diz que a criação de serviços e rotas pelo Kong Manager foi vista "anteriormente", mas isso não está no texto da aula 4. O texto também anuncia que o King entraria "em nosso arquivo de docker compose", mas o passo a passo usa Dockerfile, `docker build` e `docker run`; o Compose só aparece no fim.

## Hands On
Conhecer o **King for Kong** e analisar o **mapa de arquitetura** que ele gera com base em **Consumers**.

## Subindo o King
1. **Clonar o repositório do King** (link nas referências), porque subir pelo Dockerfile exige as configurações da aplicação.
2. Criar um **Dockerfile** para expor a aplicação (Figura 1).
3. **Build** da imagem, na raiz do repositório (Figura 2):
   ```bash
   docker build -t king .
   ```
4. **Rodar o container**:
   ```bash
   docker run --publish 4200:80 -d king
   ```
5. Abrir **`http://localhost:4500`** (Figura 3).
6. No topo, o campo **Kong node admin API**: inserir a URL do node Admin, aqui **`http://host.docker.internal:8001`**.

> [!warning] O comando publica a porta **4200**, mas o texto manda abrir **`http://localhost:4500`**. Está assim no PDF.

## O mapa de dependências
- O King cria um **map de dependências baseado em Consumers**: "todo **Consumer** é o ponto de partida no desenho de arquitetura do Kong". Útil para identificar as **dependências e ligações entre APIs** cadastradas (Figura 4).
- **Limitações**: por ser **client side**, a **administração fica difícil**, e ele **não tem tela de login**, então "acaba não sendo tão indicado".
- O **Konga** é **superior**: entrega mais funcionalidades e permite **controle de acesso** de usuários.
- Também dá para subir o King pelo **Docker Compose**; o arquivo da aula contempla o **Kong e o banco** (Figura 5).

## Referências
GitHub: ligreman/king (v3.0.10 e examples/docker_king_with_kong, v4.0.2) · Silveira (2022): Markdown
