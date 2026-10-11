# CT3: listarCategorias

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E2 |
| Como chamar | `GET /api/categorias` (com token) |

## Entrada

Não tem.

## Saída

A resposta é a própria lista (array JSON), só com as categorias ativas.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| (lista) | lista de objeto Categoria | sim | ver tabela abaixo |

**objeto Categoria**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 1 |
| name | texto | sim | Hardware |
| icon | texto | sim | monitor |
| description | texto | não | Computadores, impressoras e periféricos |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO. O Frontend volta para a tela de login. |
