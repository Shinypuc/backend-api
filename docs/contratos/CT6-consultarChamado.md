# CT6: consultarChamado

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E5, E6 e E7 |
| Como chamar | `GET /api/chamados/{ticketId}` (com token) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| ticketId | inteiro | sim | 105 |

## Saída

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| ticket | objeto Chamado | sim | ver tabela abaixo |
| timeline | lista de objeto EventoHistorico | sim | ver tabela abaixo |

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

**objeto EventoHistorico**

Um item por evento do chamado, em ordem de `createdAt` do mais antigo para o mais novo. As mensagens do chat (E6) aparecem aqui com `eventType` = COMMENT, e é isso que forma o histórico do E7.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 340 |
| ticketId | inteiro | sim | 105 |
| authorId | inteiro | sim | 7 |
| authorName | texto | sim | Carlos Mendes |
| eventType | um de: CREATION, ASSIGNMENT, STATUS_CHANGE, PRIORITY_CHANGE, COMMENT | sim | COMMENT |
| message | texto | sim | Pode reiniciar segurando o botão por 10 segundos? |
| createdAt | data e hora | sim | 2026-10-13T10:32:00 |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| O chamado não existe | HTTP 404, `error`: CHAMADO_NAO_ENCONTRADO |
| Quem chama é CLIENT e o chamado não é dele | HTTP 403, `error`: ACESSO_NEGADO |
