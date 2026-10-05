---
tags: [decisao]
status: aceita
data: 2026-09-30
---
# Decisão: SQLite em Desenvolvimento

## Contexto
Para rodar o projeto localmente era preciso instalar e configurar um MySQL 8.

## Decisão
Com `DB_DIALECT=sqlite` no `.env`, o Sequelize usa SQLite no arquivo `DB_STORAGE` (padrão `dev.sqlite`, ignorado pelo git). Sem essa variável, o banco é o MySQL. Produção continua em MySQL ([[Stack e Ambiente]]).

## Justificativa
Permite clonar, migrar e rodar o projeto sem instalar um servidor de banco.

## Consequências
- A migration de `tipo_atividade` usa `COLLATE NOCASE` no SQLite em vez de `utf8mb4_0900_as_ci`. O NOCASE só ignora maiúsculas em ASCII, então "É" e "é" contam como nomes diferentes ([[RF 5.4]]).
- A busca de clientes com `LIKE` diferencia acentos no SQLite ([[RF 3.8]]).
- Regras que dependem de collation ou de CHECK devem ser testadas também no MySQL antes da entrega.
