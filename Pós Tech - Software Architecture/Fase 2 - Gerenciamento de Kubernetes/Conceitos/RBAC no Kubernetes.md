---
tags: [pos-tech/fase-2, kubernetes, seguranca, aws, conceito]
aliases: [RBAC, IAM, ClusterRole, RoleBinding, ClusterRoleBinding, ServiceAccount]
---

# RBAC no Kubernetes

Duas formas de segurança citadas para o EKS:

| | IAM (AWS) | RBAC |
|---|---|---|
| O que é | **Gerenciamento de identidade e acesso** da AWS | **Controle de acesso baseado em função** |
| O que faz | Cria **identidades** (usuários, grupos, funções) e concede **permissões** sobre os recursos do EKS | Define **permissões granulares** para usuários ou grupos no cluster |
| Detalhes | Autenticação com **credenciais de usuário da AWS** ou **temporárias**; **autenticação baseada em funções** (assumir uma função) | **Regras personalizadas** baseadas em namespaces, Pods, serviços e outros recursos |

**Exemplo do PDF, usado para os dois**: uma função que pode **criar e excluir Pods**, mas **não pode modificar nem excluir outros recursos**.

**Objetos usados nas aulas**
- **ClusterRole**: as regras (`apiGroups`, `resources`, `verbs`). Ex.: `exemple-role`, com `get`, `watch` e `list` em `pods`.
- **RoleBinding**: associa a role a um usuário. Ex.: `exemple-rolebinding` → usuário `tadriano`.
- **Conferir**: `kubectl auth can-i get pods --as tadriano`. → [[K8S2 08 - Segurança do AWS EKS]]
- No EFK, o Fluentd usa **ServiceAccount + ClusterRole** (`get`, `list`, `watch` em `pods` e `namespaces`) **+ ClusterRoleBinding** ([[K8S2 02 - Logs e monitoramento com EFK]]).

Aparece em: [[K8S2 08 - Segurança do AWS EKS]]
