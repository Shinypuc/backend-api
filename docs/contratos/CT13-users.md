# CT13: users

| Linha | Valor |
|---|---|
| Fronteira | Banco |
| Quem chama | Backend API (lê e grava). O Backend Socket só lê, para conferir o perfil de quem conecta. |
| Quem responde | Banco |
| Atende | E1, E5, E8 e E10 |
| Como chamar | Tabela `users`, chave `id` |

## Entrada e saída

Os campos gravados são os mesmos campos lidos.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 12 |
| name | texto | sim | Ana Souza |
| email | texto | sim | ana.souza@empresa.com |
| password_hash | texto | sim | 9f2c1a...e7 (SHA-256 com salt) |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | CLIENT |
| department | texto | não | Financeiro |
| job_title | texto | não | Analista Financeira |
| avatar_url | texto | não | https://exemplo.com/ana.png |
| is_active | booleano | sim | true |
| created_at | data e hora | sim | 2026-09-01T08:00:00 |
| updated_at | data e hora | sim | 2026-10-13T10:30:00 |

`password_hash` nunca sai do Backend API: nenhuma operação HTTP devolve esse campo.

## Erros

| Quando | O que volta |
|---|---|
| `email` repetido | O banco recusa a gravação (UNIQUE). O Backend API devolve EMAIL_JA_CADASTRADO. |
| `role` fora da lista | O banco recusa a gravação (CHECK) |
| Apagar usuário que tem chamados | O banco recusa (ON DELETE RESTRICT). Por isso o E8 desativa em vez de apagar. |
