---
tags: [decisao]
status: aceita
data: 2026-11-11
---
# Decisão: Deploy com Docker e Caddy

## Contexto
O sistema precisa rodar na VPS da Hostinger (Ubuntu) já contratada, com HTTPS e num subdomínio próprio ("agenda"), ainda sem domínio comprado. A mesma VPS deve poder receber outros projetos depois.

## Decisão
- Aplicação e banco em containers, definidos no `docker-compose.yml` do repositório: `agenda-app` (Express servindo a API e o build do React) e `agenda-db` (`mysql:8.4`, dados no volume `db_data`).
- **Caddy** como proxy reverso, num docker-compose separado em `/opt/proxy` (arquivos de exemplo em `deploy/proxy/` no repositório). É o único container com portas abertas (80/443) e emite e renova o certificado HTTPS sozinho.
- Duas redes Docker: `proxy`, entre o Caddy e os apps, e `interna`, entre o app e o MySQL.
- Subdomínio provisório pelo sslip.io (`agenda.187-41-125-189.sslip.io`), que resolve direto para o IP sem configurar DNS.

## Justificativa
- O Docker deixa o ambiente igual em qualquer máquina e simplifica subir e atualizar a aplicação na VPS.
- O Caddy resolve o HTTPS sem configuração manual de certificado, o que atende ao RNF-6 (cookie `secure` em produção).
- Com o proxy separado do app, um projeto novo só precisa entrar na rede `proxy` e ganhar um bloco no `Caddyfile`, sem mexer no compose da agenda.
- Com o MySQL só na rede `interna`, o banco não fica exposto na internet.

## Consequências
- Quando houver domínio próprio, basta criar o registro A e trocar o nome no `Caddyfile`.
- O volume `caddy_data` guarda os certificados e não pode ser apagado.
- Passo a passo do deploy em `Claude outputs/DEPLOY.md`.

Ver: [[Stack e Ambiente]], [[Decisão - Arquitetura Monolítica]]
