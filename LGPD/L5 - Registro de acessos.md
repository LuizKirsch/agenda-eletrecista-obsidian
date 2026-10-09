---
tags: [lgpd, ajuste]
id: "L5"
tipo: requisito
base: "Marco Civil art. 15; LGPD art. 7º, II"
status: aceito
decisao: "RF 2.14, RF 2.15"
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
- [x] Definir número de RF (módulo 2)

## Decisão
Aceito como [[RF 2.14]] e [[RF 2.15]], com [[P2.5 - Registrar acesso]] (RN 44 e RN 45) e a nova entidade [[Registro de Acesso]]. Só logins com sucesso; expurgo automático dos registros com mais de 6 meses.

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
