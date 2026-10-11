# CT14: categories

| Linha | Valor |
|---|---|
| Fronteira | Banco |
| Quem chama | Backend API, que é o único módulo que lê e grava nesta tabela |
| Quem responde | Banco |
| Atende | E2 e E9 |
| Como chamar | Tabela `categories`, chave `id` |

## Entrada e saída

Os campos gravados são os mesmos campos lidos. As categorias iniciais (Hardware, Software, Rede, Acesso, E-mail, Outros) entram por script de carga.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 1 |
| name | texto | sim | Hardware |
| icon | texto | sim | monitor |
| description | texto | não | Computadores, impressoras e periféricos |
| is_active | booleano | sim | true |
| created_at | data e hora | sim | 2026-09-01T08:00:00 |

## Erros

| Quando | O que volta |
|---|---|
| `name` repetido | O banco recusa a gravação (UNIQUE) |
| Categoria apagada com chamados ligados | O banco grava `category_id` = nulo nesses chamados (ON DELETE SET NULL) |
