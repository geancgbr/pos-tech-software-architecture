---
tags: [pos-tech/fase-2, kubernetes, aula]
disciplina: Kubernetes
parte: 2
aula: 8
fonte: "Kubernetes parte 2/Aula 8.pdf (Thiago Adriano)"
---

# K8S2 08 - Segurança do AWS EKS

← [[K8S2 07 - Kubernetes CI-CD]] · [[Kubernetes]] · Próxima → [[K8S2 09 - Monitoramento e logging do EKS]]

> [!summary] Em uma frase
> Segurança ao criar um cluster no EKS: o **IAM** da AWS gerencia identidades (usuários, grupos e funções) e suas permissões nos recursos do EKS. O **[[RBAC no Kubernetes|RBAC]]** define **permissões granulares** por usuário ou grupo, com regras baseadas em namespaces, Pods, serviços e outros recursos.

## Hands On
Usar o **controle de acesso baseado em funções (RBAC)** para criar políticas de segurança **a nível de usuário** num cluster EKS.

## IAM (gerenciamento de identidade e acesso)
- Uma das **principais considerações de segurança** do EKS.
- Cria e gerencia **identidades de usuários, grupos e funções** que acessam os recursos do EKS, com **permissões específicas**.
- **Exemplo**: uma função no IAM que pode **criar e excluir Pods**, mas **não pode modificar nem excluir outros recursos** do cluster. Só usuários autorizados acessam os recursos, reduzindo o risco de violações.
- **Autenticação e autorização**: com **credenciais de usuário da AWS** ou **credenciais de acesso temporário**.
- **Autenticação baseada em funções**: o usuário **assume uma função** com permissões definidas.

## RBAC (controle de acesso baseado em função)
- Define **permissões granulares** para usuários ou grupos no EKS: só os autorizados acessam e modificam recursos do cluster.
- Atribui **funções** a usuários ou grupos, cada uma com suas permissões. O exemplo do PDF é o mesmo do IAM: criar e excluir Pods sem poder modificar ou excluir outros recursos.
- Permite **regras de acesso personalizadas**, baseadas em **namespaces, Pods, serviços** e outros recursos.
- Ver a **Figura 1 do PDF** ("RBAC").

## Exemplo prático
**`exemplo-role.yaml`**: uma **ClusterRole** chamada `exemple-role` com permissão de **`get`, `watch` e `list`** sobre **Pods**.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: exemple-role
rules:
- apiGroups: [""]
  resources:
  - pods
  verbs:
  - get
  - watch
  - list
```

**`example-rolebinding.yaml`**: um **RoleBinding** `exemple-rolebinding` (namespace `default`) que associa a função `exemple-role` ao usuário **`tadriano`**.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: exemple-rolebinding
  namespace: default
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: exemple-role
subjects:
- kind: User
  name: tadriano
```

**Comandos**
```bash
kubectl apply -f example-role.yaml
kubectl apply -f example-rolebinding.yaml
kubectl get clusterrole example-role          # confere a função
kubectl get rolebinding example-rolebinding   # confere o vínculo
kubectl auth can-i get pods --as tadriano     # o usuário tem a permissão? (Figura 4)
```
- Depois, **removendo o `get`** do arquivo da role e repetindo o fluxo, a permissão aparece como removida (**Figura 5**).
- As permissões devem seguir as **necessidades do aplicativo** e as **melhores práticas de segurança**.

> [!warning] Inconsistências do próprio PDF
> - Os nomes variam entre **"exemple"** (nos YAML) e **"example"** (nos comandos), e o arquivo da role aparece como `exemplo-role.yaml` e como `example-role.yaml`.
> - O texto diz que `tadriano` "terá permissão para **acessar e modificar** os Pods", mas os verbos da role são só **`get`, `watch` e `list`**.
> - Nos YAML, o `apiGroups` aparece quebrado na extração (`""` e `-` em linhas separadas). Acima, ele foi escrito como `[""]`.

## Referência
Dobies, *Operadores do Kubernetes* (Novatec, 2020)
