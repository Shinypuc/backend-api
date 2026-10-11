# CT1: autenticarUsuario

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend |
| Quem responde | Backend API |
| Atende | E1 |
| Como chamar | `POST /api/login` (sem token) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| email | texto | sim | ana.souza@empresa.com |
| password | texto | sim | Senha@123 |

## Saída

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| token | texto | sim | eyJ1c2VySWQiOjEyfQ.a1b2c3 |
| user | objeto Usuario | sim | ver tabela abaixo |

**objeto Usuario**

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 12 |
| name | texto | sim | Ana Souza |
| email | texto | sim | ana.souza@empresa.com |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | CLIENT |
| department | texto | não | Financeiro |
| jobTitle | texto | não | Analista Financeira |
| isActive | booleano | sim | true |

O token vale 24 horas e vai em todas as outras chamadas no cabeçalho `Authorization: Bearer <token>`.

## Erros

| Quando | O que volta |
|---|---|
| Falta e-mail ou senha | HTTP 400, `error`: CAMPOS_OBRIGATORIOS |
| E-mail não cadastrado ou senha errada | HTTP 401, `error`: CREDENCIAIS_INVALIDAS. O Frontend mostra a mensagem de erro na tela de login. |
| Usuário desativado pelo administrador | HTTP 403, `error`: USUARIO_INATIVO |
