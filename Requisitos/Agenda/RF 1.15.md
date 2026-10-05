---
tags: [requisito]
id: "RF 1.15"
modulo: "[[Agenda]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: parcial
---
# RF 1.15

atividades concluídas ou canceladas não podem ser arrastadas, deslocadas pela remarcação da OS nem alteradas ou removidas na edição da OS; a exclusão delas é feita somente pelo detalhe da OS ([[RF 1.25]]) (alterado: decisão do projeto);

**Módulo:** [[Agenda]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]]

**Implementação:** arraste e remarcação já bloqueiam concluídas/canceladas, mas na edição da OS elas aparecem como linhas editáveis e removíveis, e `PUT /api/os/:id` não confere o status. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
