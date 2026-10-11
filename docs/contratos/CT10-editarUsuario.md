# CT10: editarUsuario

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend (painel do administrador) |
| Quem responde | Backend API |
| Atende | E8 |
| Como chamar | `PUT /api/users/{userId}` (com token, só ADMIN) |

## Entrada

Só os campos enviados são alterados. Desativar uma conta é mandar `isActive` = false; o usuário não é apagado, porque os chamados dele continuam no histórico.

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| userId | inteiro | sim | 7 |
| name | texto | não | Carlos Mendes |
| role | um de: CLIENT, SUPPORT, ADMIN | não | ADMIN |
| department | texto | não | TI |
| jobTitle | texto | não | Coordenador de Suporte |
| isActive | booleano | não | false |

## Saída

O usuário como ficou, em objeto Usuario.

**objeto Usuario**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 7 |
| name | texto | sim | Carlos Mendes |
| email | texto | sim | carlos.mendes@empresa.com |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | ADMIN |
| department | texto | não | TI |
| jobTitle | texto | não | Coordenador de Suporte |
| isActive | booleano | sim | true |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Quem chama não é ADMIN | HTTP 403, `error`: ACESSO_NEGADO |
| O usuário não existe | HTTP 404, `error`: USUARIO_NAO_ENCONTRADO |
| `role` fora da lista | HTTP 400, `error`: PERFIL_INVALIDO |
| O administrador tenta tirar o próprio perfil ADMIN ou desativar a si mesmo | HTTP 409, `error`: AUTO_REBAIXAMENTO |
