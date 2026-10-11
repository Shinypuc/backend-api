# Contratos do Backend API

Os fluxos e a visão geral ficam no repositório do frontend: https://github.com/Vinicius-Heinzl/pi4-0102-g2-frontend/tree/main/docs/fluxos

Os contratos CT18 a CT22 (tempo real) ficam no repositório do backend-socket.

## Regras que valem para todas as fichas HTTP

- Endereço base: `https://help-desk-pi-iv.onrender.com`.
- Corpo de entrada e de saída em JSON.
- Toda operação, menos CT1 e CT2, exige o cabeçalho `Authorization: Bearer <token>`.
- Todo erro volta com o código HTTP da tabela e o corpo `{"error": "<CÓDIGO>"}`. O Frontend traduz o código para a mensagem da tela.

## Índice

| ID | Nome | Fronteira | Quem chama → quem responde | Atende |
|---|---|---|---|---|
| CT1 | [autenticarUsuario](CT1-autenticarUsuario.md) | HTTP | Frontend → Backend API | E1 |
| CT2 | [cadastrarUsuario](CT2-cadastrarUsuario.md) | HTTP | Frontend → Backend API | E1 |
| CT3 | [listarCategorias](CT3-listarCategorias.md) | HTTP | Frontend → Backend API | E2 |
| CT4 | [abrirChamado](CT4-abrirChamado.md) | HTTP | Frontend → Backend API | E2 |
| CT5 | [listarChamados](CT5-listarChamados.md) | HTTP | Frontend → Backend API | E3, E4, E9, E10 |
| CT6 | [consultarChamado](CT6-consultarChamado.md) | HTTP | Frontend → Backend API | E5, E6, E7 |
| CT7 | [atualizarChamado](CT7-atualizarChamado.md) | HTTP | Frontend → Backend API | E5 |
| CT8 | [listarUsuarios](CT8-listarUsuarios.md) | HTTP | Frontend → Backend API | E5, E8 |
| CT9 | [criarUsuario](CT9-criarUsuario.md) | HTTP | Frontend → Backend API | E8 |
| CT10 | [editarUsuario](CT10-editarUsuario.md) | HTTP | Frontend → Backend API | E8 |
| CT11 | [listarNotificacoes](CT11-listarNotificacoes.md) | HTTP | Frontend → Backend API | E5, E6 |
| CT12 | [marcarNotificacaoLida](CT12-marcarNotificacaoLida.md) | HTTP | Frontend → Backend API | E5, E6 |
| CT13 | [users](CT13-users.md) | Banco | Backend API, Backend Socket → Banco | E1, E5, E8, E10 |
| CT14 | [categories](CT14-categories.md) | Banco | Backend API → Banco | E2, E9 |
| CT15 | [tickets](CT15-tickets.md) | Banco | Backend API, Backend Socket → Banco | E2 a E6, E9, E10 |
| CT16 | [ticket_timeline](CT16-ticket_timeline.md) | Banco | Backend API, Backend Socket → Banco | E5, E6, E7 |
| CT17 | [notifications](CT17-notifications.md) | Banco | Backend API, Backend Socket → Banco | E5, E6 |
