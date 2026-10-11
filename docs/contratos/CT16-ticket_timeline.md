# CT16: ticket_timeline

| Linha | Valor |
|---|---|
| Fronteira | Banco |
| Quem chama | Backend API (grava CREATION, ASSIGNMENT e STATUS_CHANGE; lê tudo para o histórico) e Backend Socket (grava COMMENT, as mensagens do chat) |
| Quem responde | Banco |
| Atende | E5, E6 e E7 |
| Como chamar | Tabela `ticket_timeline`, chave `id` |

## Entrada e saída

Os campos gravados são os mesmos campos lidos. Nenhum evento é alterado ou apagado depois de gravado: a tabela é o histórico do atendimento (E7).

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 340 |
| ticket_id | inteiro | sim | 105 |
| author_id | inteiro | sim | 7 |
| event_type | um de: CREATION, ASSIGNMENT, STATUS_CHANGE, PRIORITY_CHANGE, COMMENT | sim | COMMENT |
| message | texto | sim | Pode reiniciar segurando o botão por 10 segundos? |
| created_at | data e hora | sim | 2026-10-13T10:32:00 |

## Erros

| Quando | O que volta |
|---|---|
| `ticket_id` ou `author_id` não existe | O banco recusa a gravação (chave estrangeira) |
| `event_type` fora da lista | O banco recusa a gravação (CHECK) |
