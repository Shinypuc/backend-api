# CT9: criarUsuario

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend (painel do administrador) |
| Quem responde | Backend API |
| Atende | E8 |
| Como chamar | `POST /api/users` (com token, só ADMIN) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| name | texto | sim | Carlos Mendes |
| email | texto | sim | carlos.mendes@empresa.com |
| password | texto | sim | Temp@2026 |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | SUPPORT |
| department | texto | não | TI |
| jobTitle | texto | não | Analista de Suporte |

## Saída

O usuário criado, como objeto Usuario.

**objeto Usuario**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 7 |
| name | texto | sim | Carlos Mendes |
| email | texto | sim | carlos.mendes@empresa.com |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | SUPPORT |
| department | texto | não | TI |
| jobTitle | texto | não | Analista de Suporte |
| isActive | booleano | sim | true |

## Erros

| Quando | O que volta |
|---|---|
| Token ausente, adulterado ou vencido | HTTP 401, `error`: TOKEN_INVALIDO |
| Quem chama não é ADMIN | HTTP 403, `error`: ACESSO_NEGADO |
| Falta nome, e-mail, senha ou perfil | HTTP 400, `error`: CAMPOS_OBRIGATORIOS |
| E-mail fora do formato nome@dominio | HTTP 400, `error`: EMAIL_INVALIDO |
| Senha com menos de 8 caracteres | HTTP 400, `error`: SENHA_FRACA |
| `role` fora da lista | HTTP 400, `error`: PERFIL_INVALIDO |
| E-mail já cadastrado | HTTP 409, `error`: EMAIL_JA_CADASTRADO |
