---
tags: [lgpd, ajuste]
id: "L5"
tipo: requisito
base: "Marco Civil art. 15; LGPD art. 7º, II"
status: a analisar
decisao:
---
# L5 – Registro de acessos (6 meses)

**Base:** Marco Civil art. 15; LGPD art. 7º, II · **Tipo:** requisito novo

## O que a apresentação propõe
Registrar IP, data e hora de cada login dos usuários e apagar os registros após 6 meses.

## Por que não estava no projeto
O sistema não guarda nenhum registro de acesso hoje.

## Onde impacta
- [[Usuários e Acesso]] e [[P2.1 - Autenticar]]
- Domínio — nova entidade/tabela de registro de acesso
- [[API REST]] — gravação no login
- [[Requisitos Não Funcionais]] — possível ajuste no RNF-6

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir rotina de expurgo dos 6 meses
- [ ] Definir número de RF (módulo 2)

## Decisão
_A preencher após a análise._

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
