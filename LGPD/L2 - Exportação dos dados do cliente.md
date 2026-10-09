---
tags: [lgpd, ajuste]
id: "L2"
tipo: requisito
base: "LGPD art. 18, V"
status: aceito
decisao: "RF 3.14"
---
# L2 – Exportação dos dados do cliente

**Base:** LGPD art. 18, V · **Tipo:** requisito novo

## O que a apresentação propõe
Exportar os dados de um cliente (cadastro, endereços, observações e OS) em JSON e CSV.

## Por que não estava no projeto
O projeto não previa nenhuma exportação; a portabilidade é direito do titular.

## Onde impacta
- [[Cliente e Endereço]] — nova ação na ficha do cliente
- [[API REST]] — nova rota de exportação
- [[Backlog]] — novo item

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir formato(s) realmente necessários (JSON, CSV ou ambos)
- [x] Definir número de RF (módulo 3)

## Decisão
Aceito como [[RF 3.14]], com os dois formatos propostos (JSON e CSV). Regras em [[P3.5 - Atender pedido do titular]] (RN 49 e RN 50).

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
