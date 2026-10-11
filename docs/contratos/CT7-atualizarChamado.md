# CT7: atualizarChamado

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E5 |
| Como chamar | `PUT /api/chamados/{ticketId}` (com token, só SUPPORT ou ADMIN) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| ticketId | inteiro | sim | 105 |
| status | um de: NEW, ASSIGNED, CLOSED, UNRESOLVED | sim | ASSIGNED |
| supportId | inteiro | não | 7 |
| message | texto | não | Chamado atribuído ao técnico Carlos Mendes. |

Regras de estado:

- NEW → ASSIGNED: exige `supportId`. É o "Me atribuir" do técnico, que manda o próprio id.
- ASSIGNED → CLOSED ou ASSIGNED → UNRESOLVED: encerra o chamado e preenche `closedAt`.
- CLOSED e UNRESOLVED são finais: o chamado não muda mais.

O Backend API grava um evento em `ticket_timeline` (ASSIGNMENT ou STATUS_CHANGE) com `message`, cria a notificação para o solicitante e avisa o Backend Socket com publicarEvento (CT18), `action` = UPDATED.

## Saída

O chamado atualizado, como objeto Chamado.

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

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Quem chama é CLIENT | HTTP 403, `error`: ACESSO_NEGADO |
| O chamado não existe | HTTP 404, `error`: CHAMADO_NAO_ENCONTRADO |
| `status` fora da lista | HTTP 400, `error`: STATUS_INVALIDO |
| Pedido de ASSIGNED sem `supportId` | HTTP 400, `error`: TECNICO_OBRIGATORIO |
| `supportId` não é de um usuário SUPPORT ou ADMIN ativo | HTTP 400, `error`: TECNICO_INVALIDO |
| O chamado já está CLOSED ou UNRESOLVED | HTTP 409, `error`: CHAMADO_ENCERRADO |
| Pedido pula etapa (NEW direto para CLOSED) | HTTP 409, `error`: TRANSICAO_INVALIDA |
