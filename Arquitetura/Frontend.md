---
tags: [arquitetura]
---
# Frontend

React 19 + React Router + Vite em `server/client/`, sem biblioteca de UI. Em desenvolvimento, o Vite (porta 5173) faz proxy de `/api` para a API (porta 3000); em produção, o Express serve `client/dist` com fallback para o `index.html`.

## Telas e rotas
| Rota | Tela | RFs |
| --- | --- | --- |
| `/login` | Login | [[RF 2.4]] |
| `/agenda` | Visão semanal (entrada após o login) | [[RF 1.1]] a [[RF 6.7]] |
| `/clientes` | Lista com busca (debounce de 300 ms) e "Novo cliente" | [[RF 3.8]] |
| `/clientes/novo` | Cadastro de cliente | [[RF 3.1]], [[RF 3.2]] |
| `/clientes/:id` | Cliente, endereços e formulário de novo endereço | [[RF 3.3]] |
| `/enderecos/:id` | Endereço e observações | [[RF 3.5]], [[RF 3.7]] |
| `/usuarios` | Lista e formulário de usuário | [[RF 2.8]] a [[RF 2.12]] |
| (modal) | Tipos de atividade, aberto pela barra lateral ou pela agenda | [[RF 1.5]], [[RF 5.1]] a [[RF 5.8]] |

## Arquivos principais
- `auth.jsx` — contexto de sessão (`/auth/me` ao abrir); um 401 com usuário logado mostra "Sua sessão expirou".
- `api.js` — `fetch` com cookie; transforma `{ erro }` em `Error`.
- `datas.js` — mesma aritmética de datas do backend; "hoje" calculado em America/Sao_Paulo.
- `agenda/Grade.jsx` — grade de 24h (48 px por hora, bloco com altura mínima de 20 px).
- `agenda/OsForm.jsx` — criar, editar e adicionar atividade à OS.
- `agenda/DetalheAtividade.jsx` — OS aberta com a atividade selecionada e as ações.
- `agenda/RemarcarAtividade.jsx` e `agenda/Modal.jsx` — `<dialog>` nativo que fecha ao clicar fora, com animação.

## Comportamentos da agenda
- **Arraste:** com mouse, começa após mover 5 px; no toque, só depois de pressionar e segurar por 300 ms, para não atrapalhar a rolagem. Encaixa em 15 min ([[RF 1.9]]).
- **Grupos:** atividades seguidas da mesma OS que se cobririam na tela viram um bloco "N atividades · OS X"; arrastar o grupo desloca a OS inteira sem perguntar ([[RF 1.8]]).
- **Colunas:** blocos sobrepostos são distribuídos lado a lado considerando a altura mínima na tela ([[RF 1.8]]).
- **Clique em horário vazio:** abre "Nova OS" com a data e a hora cheia do slot ([[RF 1.4]]).
- **Sem tipo ativo:** ao criar OS ou adicionar atividade, abre o modal de tipos com aviso ([[RF 5.8]]).
- Toda alteração fecha o modal e recarrega a semana ([[RF 1.12]]); `aviso_conflito` mostra um aviso em destaque ([[RF 6.13]]).

## Visual
- Fontes IBM Plex Sans (texto) e JetBrains Mono (horários), via Google Fonts.
- Paleta em variáveis CSS no `:root` de `estilo.css` (primária âmbar `#894d00`, secundária `#276862`).
- Botões com 36 px de altura, que sobem para 44 px em telas com menos de 768 px ([[Requisitos Não Funcionais|RNF-7]]).

Ver: [[API REST]], [[Stack e Ambiente]]
