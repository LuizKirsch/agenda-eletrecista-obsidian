---
tags: [projeto]
---
# Histórico de Commits

Commits da branch `main` do repositório [agenda-eletrecista](https://github.com/LuizKirsch/agenda-eletrecista), agrupados por etapa. Para o histórico da documentação, ver [[Histórico de Versões]].

## 26/09/2026 — Estrutura
| Commit | Descrição |
| --- | --- |
| `88924ef` | Primeiro commit (README) |
| `03c43ac` | Estrutura do server: `app.js`, `server.js` e as pastas routes, controllers, services e models ([[Stack e Ambiente]]) |

## 27/09/2026 — Usuários e Acesso (doc V4)
| Commit | Descrição |
| --- | --- |
| `36b2693` | Sequelize, MySQL, `config/config.js` e `.env.example` |
| `f20dc58` | Migration e model de `usuario`, com a secretária inicial lida do `.env` ([[RF 2.13]]) |
| `503c96b` | API: login/logout/me com JWT em cookie, CRUD de usuários, middlewares `autenticar`, `somenteSecretaria` e `erros` ([[P2.1 - Autenticar]]) |
| `ba91ac0` | Client React + Vite: login, layout autenticado e tela de usuários |

## 27/09/2026 — Cliente e Endereço (doc V5)
| Commit | Descrição |
| --- | --- |
| `0728140` | Migrations e models de `cliente`, `endereco` e `endereco_observacao`; helper `lerCampos` (apara, valida obrigatórios e tamanhos) |
| `4b5fc36` | API: listar/buscar, cadastrar e detalhar cliente; endereços e observações ([[P3.1 - Cadastrar cliente, endereço e observação]], [[P3.2 - Buscar cliente]]) |
| `4b5d95a` | Telas de clientes, novo cliente, cliente (com endereços) e endereço (com observações) |

## 27/09/2026 — Atividade (doc V5)
| Commit | Descrição |
| --- | --- |
| `3057be1` | Migration de `tipo_atividade` com collation `utf8mb4_0900_as_ci` e CHECK de 5 a 720 min |
| `6db91fd` | API de tipos: CRUD, situação, contagem de uso, ao menos um ativo ([[P5.1 - Gerenciar tipos de atividade]]) |
| `270cbf7` | Modal de tipos de atividade, aberto pela barra lateral e pela agenda ([[RF 1.5|RF 1.7]]) |

## 27/09/2026 — Agenda (doc V5)
| Commit | Descrição |
| --- | --- |
| `2ff320e` | Migrations de `ordem_servico` e `atividade_os` (CHECK `hora_fim > hora_inicio`, índice em `data`) |
| `fb7f9b2` | API: agenda semanal, OS, deslocar a OS, concluir, remarcar/status/excluir atividade; `horario.js` ([[Decisão - Datas e Horas como Texto]]) |
| `772dc66` | Grade semanal com arraste, modais de OS, detalhe e remarcação ([[Frontend]]) |

## 30/09/2026 — Ambiente
| Commit | Descrição |
| --- | --- |
| `8c0c06f` | SQLite como banco opcional de desenvolvimento ([[Decisão - SQLite em Desenvolvimento]]); entraram também arquivos vazios por engano ([[Status da Implementação#Limpeza no repositório]]) |

## 05/10/2026 — Interface e documentação
| Commit | Descrição |
| --- | --- |
| `04db81e` | README com funcionalidades, instalação, scripts e API |
| `ce4b5bb` | Fontes IBM Plex Sans e JetBrains Mono (Google Fonts) |
| `5518334` | Nova paleta de cores e tipografia no `estilo.css` |
| `face093` | Modal fecha ao clicar fora; ajustes no layout e no login |
| `4c5b01e` | Ajuste no README |
| `32f1439` | Animação ao fechar o modal |
| `50ef569` | `CLAUDE.md` e `.claude/settings.json` apontando para este vault |
