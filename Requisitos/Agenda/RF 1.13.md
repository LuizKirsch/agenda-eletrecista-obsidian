---
tags: [requisito]
id: "RF 1.13"
modulo: "[[Agenda]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 1.13

o sistema deve permitir filtrar a agenda por eletricista, exibindo as atividades de todos ou de um ou mais eletricistas selecionados (decisão do projeto; alterado em 06/11/2026: seleção múltipla);

**Módulo:** [[Agenda]]
**Entidades:** [[Atividade da OS]], [[Usuário]]
**Implementação:** botão "Eletricistas ▾" acima da grade, com busca e checkboxes (vários ao mesmo tempo), cada eletricista com a sua cor ([[Usuário]]); o botão resume a seleção ("Edson, Ana" ou "3 selecionados"). `GET /api/agenda?eletricista_id=1,2` (06/11/2026).
**Regras:** [[P6.1 - Criar OS]]

> Origem: pedido do professor na apresentação de 28/10/2026.
