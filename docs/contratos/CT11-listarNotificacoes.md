# CT11: listarNotificacoes

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E5 e E6 |
| Como chamar | `GET /api/notificacoes` (com token) |

## Entrada

Não tem. O Backend API devolve as notificações do usuário do token.

## Saída

A resposta é a própria lista (array JSON), da mais nova para a mais antiga.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| (lista) | lista de objeto Notificacao | sim | ver tabela abaixo |

**objeto Notificacao**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 88 |
| ticketId | inteiro | não | 105 |
| type | um de: chamado_novo, status_alterado, comentario, atribuicao, resolvido | sim | atribuicao |
| title | texto | sim | Chamado atribuído |
| message | texto | sim | O chamado #0105 foi atribuído ao técnico Carlos Mendes. |
| isRead | booleano | sim | false |
| createdAt | data e hora | sim | 2026-10-13T10:30:00 |

O Frontend chama esta operação ao abrir o painel e sempre que recebe chamadoAtualizado (CT22) ou mensagemRecebida (CT21), para atualizar o sino.

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
