# CT15: tickets

| Linha | Valor |
|---|---|
| Fronteira | Banco |
| Quem chama | Backend API (lê e grava). O Backend Socket só lê, para saber quem participa do chat de um chamado. |
| Quem responde | Banco |
| Atende | E2, E3, E4, E5, E6, E9 e E10 |
| Como chamar | Tabela `tickets`, chave `id` |

## Entrada e saída

Os campos gravados são os mesmos campos lidos.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 105 |
| title | texto | sim | Notebook não liga |
| description | texto | sim | O notebook não liga desde hoje de manhã, mesmo na tomada. |
| status | um de: NEW, ASSIGNED, CLOSED, UNRESOLVED | sim | ASSIGNED |
| priority | um de: LOW, MEDIUM, HIGH, URGENT | sim | HIGH |
| category_id | inteiro | não | 1 |
| client_id | inteiro | sim | 12 |
| support_id | inteiro | não | 7 |
| created_at | data e hora | sim | 2026-10-13T09:15:00 |
| updated_at | data e hora | sim | 2026-10-13T10:30:00 |
| closed_at | data e hora | não | 2026-10-13T16:45:00 |

`updated_at` é atualizado por trigger a cada UPDATE. `closed_at` só é preenchido quando o status vira CLOSED ou UNRESOLVED.

## Erros

| Quando | O que volta |
|---|---|
| `client_id`, `support_id` ou `category_id` não existe | O banco recusa a gravação (chave estrangeira) |
| `status` ou `priority` fora da lista | O banco recusa a gravação (CHECK) |
