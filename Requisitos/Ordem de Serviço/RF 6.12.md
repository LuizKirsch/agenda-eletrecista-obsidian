---
tags: [requisito]
id: "RF 6.12"
id_v6: "RF 1.18"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Média
alterado: true
entrega: 1
implementacao: completa
---
# RF 6.12

o sistema deve sinalizar conflito quando uma atividade se sobrepuser a outra do mesmo eletricista no mesmo dia, tanto na agenda quanto no detalhe da atividade (alterado: decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Atividade da OS]], [[Usuário]]
**Implementação:** o conflito é calculado por eletricista e dia (`idsEmConflito`), com índice `idx_atividade_os_eletricista_data` (06/11/2026).

> Fonte: Documentação Técnica V6, seção 4.
> Numeração V7 (separação do módulo Ordem de Serviço); na V6: RF 1.18.
> Alterado pelo pedido do professor (28/10/2026).
