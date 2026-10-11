# CT5: listarChamados

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E3, E4, E9 e E10 |
| Como chamar | `GET /api/chamados?status=&clientId=&supportId=` (com token) |

## Entrada

Filtros opcionais na URL.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| status | um de: NEW, ASSIGNED, CLOSED, UNRESOLVED | não | NEW |
| clientId | inteiro | não | 12 |
| supportId | inteiro | não | 7 |

Regra de perfil: se quem chama é CLIENT, o Backend API ignora `clientId` e devolve só os chamados abertos por ele (E3). SUPPORT e ADMIN recebem todos os chamados que passam nos filtros (E4, E9, E10).

## Saída

A resposta é a própria lista (array JSON).

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| (lista) | lista de objeto Chamado | sim | ver tabela abaixo |

A lista vem ordenada por `createdAt`, do mais novo para o mais antigo. Lista vazia quando nada passa nos filtros.

**objeto Chamado**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 105 |
| title | texto | sim | Notebook não liga |
| description | texto | sim | O notebook não liga desde hoje de manhã, mesmo na tomada. |
| status | um de: NEW, ASSIGNED, CLOSED, UNRESOLVED | sim | ASSIGNED |
| priority | um de: LOW, MEDIUM, HIGH, URGENT | sim | HIGH |
| categoryId | inteiro | não | 1 |
| categoryName | texto | não | Hardware |
| clientId | inteiro | sim | 12 |
| clientName | texto | sim | Ana Souza |
| supportId | inteiro | não | 7 |
| supportName | texto | não | Carlos Mendes |
| createdAt | data e hora | sim | 2026-10-13T09:15:00 |
| updatedAt | data e hora | sim | 2026-10-13T10:30:00 |
| closedAt | data e hora | não | 2026-10-13T16:45:00 |

O dashboard (E9) calcula as contagens por estado e por prioridade a partir desta lista. O relatório (E10) usa `clientName`, `supportName`, `priority`, `status`, `createdAt` e `closedAt`.

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Filtro `status` fora da lista | HTTP 400, `error`: STATUS_INVALIDO |
