# CT2: cadastrarUsuario

| Linha | Valor |
|---|---|
| Fronteira | HTTP |
| Quem chama | Frontend (tela pública `register.html`) |
| Quem responde | Backend API |
| Atende | E1 |
| Como chamar | `POST /api/register` (sem token) |

## Entrada

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| name | texto | sim | Ana Souza |
| email | texto | sim | ana.souza@empresa.com |
| password | texto | sim | Senha@123 |
| department | texto | não | Financeiro |
| jobTitle | texto | não | Analista Financeira |

O perfil não é enviado: toda conta criada por esta operação nasce com `role` = CLIENT. Técnicos e administradores são criados pelo administrador na operação criarUsuario (CT9).

## Saída

| Campo | Tipo | Obrigatório | Exemplo |
|---|---|---|---|
| id | inteiro | sim | 12 |
| name | texto | sim | Ana Souza |
| email | texto | sim | ana.souza@empresa.com |
| role | um de: CLIENT, SUPPORT, ADMIN | sim | CLIENT |

## Erros

| Quando | O que volta |
|---|---|
| Falta nome, e-mail ou senha | HTTP 400, `error`: CAMPOS_OBRIGATORIOS |
| E-mail fora do formato nome@dominio | HTTP 400, `error`: EMAIL_INVALIDO |
| Senha com menos de 8 caracteres | HTTP 400, `error`: SENHA_FRACA |
| E-mail já cadastrado | HTTP 409, `error`: EMAIL_JA_CADASTRADO |
