---
tags: [requisito]
id: "RF 3.11"
modulo: "[[Cliente e Endereço]]"
prioridade: Média
alterado: false
entrega: 1
implementacao: pendente
---
# RF 3.11

o sistema deve permitir excluir cliente ou endereço, com confirmação, somente quando não houver OS vinculada a ele; excluir um cliente exclui seus endereços e observações, e excluir um endereço exclui suas observações;

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Ordem de Serviço]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** não há rota de exclusão de cliente ou endereço, e as FKs de `endereco` e `endereco_observacao` não têm ON DELETE CASCADE. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
