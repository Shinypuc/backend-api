# CT12: marcarNotificacaoLida

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E5 e E6 |
| Como chamar | `PUT /api/notificacoes/{notificationId}/read` (com token) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| notificationId | inteiro | sim | 88 |

## Saída

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 88 |
| isRead | booleano | sim | true |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| A notificação não existe | HTTP 404, `error`: NOTIFICACAO_NAO_ENCONTRADA |
| A notificação é de outro usuário | HTTP 403, `error`: ACESSO_NEGADO |
