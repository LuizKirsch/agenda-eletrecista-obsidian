---
tags: [arquitetura]
---
# Stack e Ambiente

## Tecnologias
- **Frontend:** React 19 com Vite e React Router ([[Frontend]]) (aplicação web responsiva, mobile-first)
- **Backend:** Node.js com Express 5 (API REST), integrado ao frontend em uma única base de deploy; o Express serve o build do React
- **Banco de dados:** MySQL 8.0.16 ou mais recente (necessário para a collation `utf8mb4_0900_as_ci` e para as restrições CHECK), com Sequelize (ORM) e sequelize-cli (migrations); SQLite opcional em desenvolvimento ([[Decisão - SQLite em Desenvolvimento]])
- **Autenticação:** senhas com hash bcrypt; sessão por JWT assinado em cookie httpOnly
- **Datas e horários:** trafegam como texto (`YYYY-MM-DD` e `HH:MM`), sem conversão de fuso, com fuso de referência America/Sao_Paulo ([[Decisão - Datas e Horas como Texto]])

## Infraestrutura
- Aplicação hospedada em VPS Hostinger (Ubuntu), com tudo rodando em containers Docker ([[Decisão - Deploy com Docker e Caddy]])
- **Caddy** (`caddy:2`, compose próprio em `/opt/proxy`, fora do repositório): único container com portas abertas (80/443), faz o proxy reverso e emite/renova o HTTPS (Let's Encrypt)
- **agenda-app**: Express servindo a API e o build do React (`Dockerfile` do repositório), porta interna 3000
- **agenda-db**: `mysql:8.4`, com os dados no volume `db_data`
- Redes Docker: `proxy` (Caddy ↔ app, compartilhada com projetos futuros) e `interna` (app ↔ MySQL); o MySQL não fica acessível de fora
- Endereço provisório: `agenda.187-41-125-189.sslip.io`, até ter domínio próprio
- Acesso via navegador, sem instalação de aplicativo (o Edson já abandonou ferramentas anteriores por excesso de complexidade)

## Camadas do backend (`server/`)
- **routes** — URL → controller, só isso ([[API REST]])
- **controllers** — recebem a requisição, validam, chamam o service e devolvem JSON
- **services** — regras de negócio (ver [[00 - Visão Geral#Regras de negócio|RNs]])
- **models** — Sequelize + migrations via sequelize-cli
- **middlewares** — `autenticar` (sessão), `somenteSecretaria` (perfil) e `erros` (`httpErro`, `lerCampos`, `exigirCampos`, `tratarErros`)
- **client/** — frontend React ([[Frontend]])

## Rodando
| Script | O que faz |
| --- | --- |
| `npm run dev` | API (nodemon, porta 3000) + Vite (porta 5173, com proxy de `/api`) |
| `npm run db:migrate` | Aplica as migrations (exige as variáveis `SECRETARIA_*`) |
| `npm run build` | Gera `client/dist` |
| `npm start` | Express servindo a API e o build |

Variáveis do `.env`: `DB_*` (ou `DB_DIALECT=sqlite` + `DB_STORAGE`), `JWT_SECRET` (obrigatória, o servidor não sobe sem ela), `JWT_EXPIRES_IN` (padrão 7d) e `SECRETARIA_NOME/LOGIN/SENHA`.

Ver também: [[Decisão - Arquitetura Monolítica]], [[Requisitos Não Funcionais]]

Repositório: https://github.com/LuizKirsch/agenda-eletrecista
