# CT17: notifications

| Linha | Valor |
|---|---|
| Fronteira | Banco |
| Quem chama | Backend API (grava nas mudanças de chamado; lê e marca como lida) e Backend Socket (grava a notificação de nova mensagem do chat) |
| Quem responde | Banco |
| Atende | E5 e E6 |
| Como chamar | Tabela `notifications`, chave `id` |

## Entrada e saída

Os campos gravados são os mesmos campos lidos.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 88 |
| user_id | inteiro | sim | 12 |
| ticket_id | inteiro | não | 105 |
| type | um de: chamado_novo, status_alterado, comentario, atribuicao, resolvido | sim | atribuicao |
| title | texto | sim | Chamado atribuído |
| message | texto | sim | O chamado #0105 foi atribuído ao técnico Carlos Mendes. |
| is_read | booleano | sim | false |
| created_at | data e hora | sim | 2026-10-13T10:30:00 |

## Erros

| Quando | O que volta |
|---|---|
| `user_id` ou `ticket_id` não existe | O banco recusa a gravação (chave estrangeira) |
