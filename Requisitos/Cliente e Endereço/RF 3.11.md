---
tags: [requisito]
id: "RF 3.11"
modulo: "[[Cliente e Endereço]]"
prioridade: Média
alterado: true
entrega: 1
implementacao: completa
lgpd: "[[L1 - Anonimização no lugar do bloqueio de exclusão|L1]]"
---
# RF 3.11

o sistema deve permitir excluir cliente ou endereço, com confirmação, somente quando não houver OS vinculada a ele (alterado: decisão do projeto); excluir um cliente exclui seus endereços, observações e orçamentos, e excluir um endereço exclui suas observações e os orçamentos desse endereço;

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Ordem de Serviço]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** não há rota de exclusão de cliente ou endereço, e as FKs de `endereco` e `endereco_observacao` não têm ON DELETE CASCADE. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
> V2 do app: com OS vinculada, o pedido de eliminação passa a ser atendido por anonimização ([[RF 3.13]], ajuste de LGPD [[L1 - Anonimização no lugar do bloqueio de exclusão|L1]]). Ver [[Fora do MVP#V2 do app]].

> Alterado em 27/10/2026: os orçamentos são excluídos junto. Bloquear a exclusão por orçamento prendia para sempre o cliente com orçamento aceito ou recusado, que não pode ser excluído ([[P4.3 - Editar e excluir orçamento#RN 54|RN 54]]).
