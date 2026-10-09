---
tags: [requisito, lgpd]
id: "RF 3.11"
modulo: "[[Cliente e Endereço]]"
prioridade: Média
alterado: true
entrega: 1
implementacao: pendente
lgpd: "[[L1 - Anonimização no lugar do bloqueio de exclusão|L1]]"
---
# RF 3.11

o sistema deve permitir excluir cliente ou endereço, com confirmação, somente quando não houver OS vinculada a ele; excluir um cliente exclui seus endereços e observações, e excluir um endereço exclui suas observações; quando o titular pedir a eliminação e o cliente tiver OS vinculada, o cliente deve ser anonimizado ([[RF 3.13]]) em vez de a exclusão ser bloqueada (alterado: LGPD);

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Ordem de Serviço]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** não há rota de exclusão de cliente ou endereço, e as FKs de `endereco` e `endereco_observacao` não têm ON DELETE CASCADE. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
> V7: alterado pelo ajuste de LGPD [[L1 - Anonimização no lugar do bloqueio de exclusão|L1]] (art. 18, IV) — com OS vinculada, o pedido de eliminação é atendido por anonimização.
