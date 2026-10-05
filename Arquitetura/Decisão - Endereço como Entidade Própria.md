---
tags: [decisao]
status: aceita
---
# Decisão: Endereço como Entidade Própria

## Contexto
A principal dor do Edson é a falta de histórico estruturado de clientes, endereços e orçamentos.

## Decisão
[[Endereço]] é uma entidade própria vinculada ao [[Cliente]] (1:N), com [[Observação de Endereço]] datadas ([[RF 3.3]], [[RF 3.4]], [[RF 3.5]]).

## Justificativa
O histórico do imóvel é priorizado sobre o histórico do cliente isoladamente, já que o eletricista retorna ao local, não à pessoa.
