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
| `/clientes` | Lista com busca (debounce de 300 ms); "Novo cliente" abre um diálogo e, ao salvar, vai para a ficha | [[RF 3.1]], [[RF 3.2]], [[RF 3.8]] |
| `/clientes/:id` | Cliente e endereços em cartões; "Adicionar endereço" e "Editar" abrem diálogos; "Excluir" confirma e volta à lista | [[RF 3.3]], [[RF 3.9]], [[RF 3.11]] |
| `/enderecos/:id` | Endereço e observações; "Nova observação" abre um diálogo com o aviso da [[RF 3.16]]; editar e excluir o endereço no topo e cada observação no próprio cartão | [[RF 3.5]], [[RF 3.7]], [[RF 3.10]] a [[RF 3.12]], [[RF 3.16]] |
| `/usuarios` | Tabela de usuários; novo/editar em diálogo | [[RF 2.8]] a [[RF 2.12]] |
| `/tipos-atividade` | Tabela de tipos com valor padrão; novo/editar em diálogo. A agenda redireciona para cá quando não há tipo ativo | [[RF 1.5]], [[RF 5.1]] a [[RF 5.8]] |
| `/orcamentos` | Tabela de orçamentos; "Novo orçamento" abre o formulário em painel e, ao salvar, vai para o detalhe | [[RF 4.8]] a [[RF 4.10]], [[RF 4.14]] |
| `/orcamentos/:id` | Detalhe com itens e total; pendente tem Editar, Recusar, Excluir e Aceitar (diálogo com data e início, mostra o horário de término). Aceito ou recusado fica só leitura | [[RF 4.11]] a [[RF 4.13]], [[RF 4.15]] |

## Arquivos principais
- `auth.jsx` — contexto de sessão (`/auth/me` ao abrir); um 401 com usuário logado mostra "Sua sessão expirou".
- `api.js` — `fetch` com cookie; transforma `{ erro }` em `Error`.
- `datas.js` — mesma aritmética de datas do backend; "hoje" calculado em America/Sao_Paulo.
- `agenda/Grade.jsx` — grade de 24h (48 px por hora, bloco com altura mínima de 20 px).
- `agenda/OsForm.jsx` — criar, editar e adicionar atividade à OS; a atividade avulsa aparece com a descrição no lugar do tipo. Com qualquer informação preenchida, toda forma de fechar pede confirmação ([[RF 6.20]]).
- `pages/OrcamentoForm.jsx` — criar e editar orçamento; o item começa sem atividade escolhida (obrigatório escolher um tipo ou "Avulso"); ao escolher o tipo, copia nome e valor padrão e sugere o tempo como quantidade × duração padrão ([[RF 4.9]]). Com qualquer informação preenchida, toda forma de fechar (Cancelar, ×, clique fora, Esc) pede confirmação ([[RF 4.16]]).
- `agenda/Modal.jsx` — também exporta `Confirmar` (confirmação de ação destrutiva no lugar do `window.confirm`); a prop `confirmarSaida` do `Modal` ativa a pergunta antes de fechar.
- `formato.js` — endereço, data/hora, reais (`formatarReais`) e duração (`formatarDuracao`).
- `agenda/DetalheAtividade.jsx` — OS aberta com a atividade selecionada e as ações.
- `agenda/RemarcarAtividade.jsx` e `agenda/Modal.jsx` — `<dialog>` nativo que fecha ao clicar fora, com animação.

## Comportamentos da agenda
- **Arraste:** com mouse, começa após mover 5 px; no toque, só depois de pressionar e segurar por 300 ms, para não atrapalhar a rolagem. Encaixa em 15 min ([[RF 1.9]]).
- **Grupos:** atividades seguidas da mesma OS que se cobririam na tela viram um bloco "N atividades · OS X"; arrastar o grupo desloca a OS inteira sem perguntar ([[RF 1.8]]).
- **Colunas:** blocos sobrepostos são distribuídos lado a lado considerando a altura mínima na tela ([[RF 1.8]]).
- **Vinda do orçamento aceito:** "Ver na agenda" abre a semana da data escolhida no aceite (`state.data`).
- **Clique em horário vazio:** abre "Nova OS" com a data e a hora cheia do slot ([[RF 1.4]]).
- **Sem tipo ativo:** ao criar OS ou adicionar atividade, abre o modal de tipos com aviso ([[RF 5.8]]).
- Toda alteração fecha o modal e recarrega a semana ([[RF 1.12]]); `aviso_conflito` mostra um aviso em destaque ([[RF 6.13]]).

## Visual
- Fonte Inter, via Google Fonts; ícones em SVG inline (`icones.jsx`).
- Visual flat: superfícies brancas com borda fina sobre fundo cinza-claro, tokens no `:root` de `estilo.css`; cor principal verde-petróleo `#0f766e`, âmbar só na marca.
- Listas e formulários separados: a página mostra a lista e o cadastro/edição abre em `Modal` (variante `dialogo`, centralizado; ou `painel`, à direita).
- Celular (< 768 px): barra inferior com Agenda, Clientes, Orçamentos, Tipos e Usuários; conta e "Sair" no avatar do topo; tabelas viram cartões; diálogos viram folhas que sobem de baixo.
- Agenda no celular: faixa com os 7 dias e lista só com os horários agendados (`agenda/ListaSemana.jsx`), sem arraste; remarcar pelo detalhe da OS.
- Botões com 40 px de altura, que sobem para 44 px em telas com menos de 768 px ([[Requisitos Não Funcionais|RNF-7]]).

Ver: [[API REST]], [[Stack e Ambiente]]
