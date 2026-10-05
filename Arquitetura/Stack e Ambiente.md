---
tags: [arquitetura]
---
# Stack e Ambiente

## Tecnologias
- **Frontend:** React com Vite e React Router (aplicação web responsiva, mobile-first)
- **Backend:** Node.js com Express 5 (API REST), integrado ao frontend em uma única base de deploy; o Express serve o build do React
- **Banco de dados:** MySQL 8.0.16 ou mais recente (necessário para a collation `utf8mb4_0900_as_ci` e para as restrições CHECK), com Sequelize (ORM) e sequelize-cli (migrations)
- **Autenticação:** senhas com hash bcrypt; sessão por JWT assinado em cookie httpOnly
- **Datas e horários:** trafegam como texto (`YYYY-MM-DD` e `HH:MM`), sem conversão de fuso, com fuso de referência America/Sao_Paulo

## Infraestrutura
- Aplicação hospedada em VPS (servidor de aplicação e servidor web/HTTP no mesmo ambiente)
- Acesso via navegador, sem instalação de aplicativo (o Edson já abandonou ferramentas anteriores por excesso de complexidade)

## Camadas do backend (`server/`)
- **routes** — URL → controller, só isso
- **controllers** — recebem a requisição, validam, chamam o service e devolvem JSON
- **services** — regras de negócio (ver [[00 - Visão Geral#Regras de negócio|RNs]])
- **models** — Sequelize + migrations via sequelize-cli

Ver também: [[Decisão - Arquitetura Monolítica]], [[Requisitos Não Funcionais]]

Repositório: https://github.com/LuizKirsch/agenda-eletrecista
