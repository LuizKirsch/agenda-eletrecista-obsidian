---
tags: [requisito]
id: "RF 6.11"
id_v6: "RF 1.15"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: parcial
---
# RF 6.11

atividades concluídas ou canceladas não podem ser arrastadas, deslocadas pela remarcação da OS nem alteradas ou removidas na edição da OS; a exclusão delas é feita somente pelo detalhe da OS ([[RF 6.17]]) (alterado: decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]]

**Implementação:** arraste e remarcação já bloqueiam concluídas/canceladas, mas na edição da OS elas aparecem como linhas editáveis e removíveis, e `PUT /api/os/:id` não confere o status. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
> Numeração V7 (separação do módulo Ordem de Serviço); na V6: RF 1.15.
