---
tags: [lgpd, ajuste]
id: "L6"
tipo: regra
base: "LGPD art. 15 e 16; CDC art. 27"
status: a analisar
decisao:
---
# L6 – Política de retenção

**Base:** LGPD art. 15 e 16; CDC art. 27 · **Tipo:** regra de negócio / processo

## O que a apresentação propõe
Guardar cliente, endereço, observações e OS por 5 anos após o último serviço (prazo do art. 27 do CDC); usuários enquanto ativos; registros de acesso por 6 meses.

## Por que não estava no projeto
O projeto não define quando os dados deixam de ser necessários. O [[Requisitos Não Funcionais|RNF-5]] só fala em persistência e backup.

## Onde impacta
- [[Requisitos Não Funcionais]] — RNF-5
- [[Cliente]] / [[Ordem de Serviço]] — data do último serviço
- Liga com a [[L1 - Anonimização no lugar do bloqueio de exclusão|L1]] (o que fazer ao fim do prazo)

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Decidir se o expurgo/anonimização ao fim do prazo é automático ou manual

## Decisão
_A preencher após a análise._

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
