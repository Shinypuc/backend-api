# CT8: listarUsuarios

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E5 e E8 |
| Como chamar | `GET /api/users?role=` (com token, só SUPPORT ou ADMIN) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| role | um de: CLIENT, SUPPORT, ADMIN | não | SUPPORT |

No E5 o Frontend pede `role` = SUPPORT para montar a lista de técnicos. No E8 o administrador pede sem filtro.

## Saída

A resposta é a própria lista (array JSON).

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| (lista) | lista de objeto Usuario | sim | ver tabela abaixo |

**objeto Usuario**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 7 |
| name | texto | sim | Carlos Mendes |
| email | texto | sim | carlos.mendes@empresa.com |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | SUPPORT |
| department | texto | não | TI |
| jobTitle | texto | não | Analista de Suporte |
| isActive | booleano | sim | true |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Quem chama é CLIENT | HTTP 403, `error`: ACESSO_NEGADO |
| Filtro `role` fora da lista | HTTP 400, `error`: PERFIL_INVALIDO |
