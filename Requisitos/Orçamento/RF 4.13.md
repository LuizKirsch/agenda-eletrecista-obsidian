---
tags: [requisito]
id: "RF 4.13"
modulo: "[[Orçamento (módulo)]]"
prioridade: Alta
alterado: true
entrega: 2
implementacao: parcial
---
# RF 4.13

ao aceitar um orçamento, o sistema deve gerar uma OS com o cliente e o endereço do orçamento e uma atividade agendada para cada item de serviço, na ordem dos itens e com a duração igual ao tempo do item; o eletricista é escolhido no aceite e pode ser trocado por atividade, as atividades são recomendadas a partir da data e do horário de início informados sem sobrepor a agenda do eletricista ([[RF 4.19]]), e o usuário pode ajustar a data e o início de cada uma antes de confirmar, de modo que a OS pode ocupar vários dias (alterado: decisão do projeto); itens avulsos geram atividades avulsas, e a OS fica vinculada ao orçamento ([[RF 4.7]]);

**Módulo:** [[Orçamento (módulo)|Orçamento]]
**Entidades:** [[Orçamento]], [[Item de Serviço]], [[Ordem de Serviço]], [[Atividade da OS]]
**Regras:** [[P4.2 - Aceitar ou recusar orçamento]]

> Origem: decisão do projeto (19/10/2026). Ver [[Proposta - Modelo do Orçamento]].
> Alterado pelo pedido do professor (28/10/2026).
