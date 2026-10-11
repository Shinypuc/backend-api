# CT4: abrirChamado

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E2 |
| Como chamar | `POST /api/chamados` (com token) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| title | texto | sim | Notebook não liga |
| description | texto | sim | O notebook não liga desde hoje de manhã, mesmo na tomada. |
| priority | um de: LOW, MEDIUM, HIGH, URGENT | sim | HIGH |
| categoryId | inteiro | sim | 1 |

O solicitante não é enviado: o Backend API usa o usuário do token como `clientId`. O chamado sempre nasce com `status` = NEW e sem técnico.

## Saída

O chamado criado, como objeto Chamado.

**objeto Chamado**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 105 |
| title | texto | sim | Notebook não liga |
| description | texto | sim | O notebook não liga desde hoje de manhã, mesmo na tomada. |
| status | um de: NEW, ASSIGNED, CLOSED, UNRESOLVED | sim | NEW |
| priority | um de: LOW, MEDIUM, HIGH, URGENT | sim | HIGH |
| categoryId | inteiro | não | 1 |
| categoryName | texto | não | Hardware |
| clientId | inteiro | sim | 12 |
| clientName | texto | sim | Ana Souza |
| supportId | inteiro | não | 7 |
| supportName | texto | não | Carlos Mendes |
| createdAt | data e hora | sim | 2026-10-13T09:15:00 |
| updatedAt | data e hora | sim | 2026-10-13T09:15:00 |
| closedAt | data e hora | não | 2026-10-13T16:45:00 |

Depois de gravar, o Backend API avisa o Backend Socket com publicarEvento (CT18), `action` = CREATED.

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Falta título, descrição, prioridade ou categoria | HTTP 400, `error`: CAMPOS_OBRIGATORIOS |
| Prioridade fora da lista | HTTP 400, `error`: PRIORIDADE_INVALIDA |
| A categoria não existe ou está inativa | HTTP 400, `error`: CATEGORIA_INVALIDA |
