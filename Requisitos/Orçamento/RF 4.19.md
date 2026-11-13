---
tags: [requisito]
id: "RF 4.19"
modulo: "[[Orçamento (módulo)]]"
prioridade: Alta
alterado: true
entrega: 2
implementacao: completa
---
# RF 4.19

no aceite do orçamento, o sistema deve recomendar data e horário para cada atividade a ser gerada sem sobrepor atividades já agendadas do eletricista escolhido (decisão do projeto);

**Módulo:** [[Orçamento (módulo)|Orçamento]]
**Entidades:** [[Orçamento]], [[Item de Serviço]], [[Atividade da OS]], [[Usuário]]
**Implementação:** `services/recomendacao.js` (função pura, first-fit da [[P4.2 - Aceitar ou recusar orçamento#RN 67|RN 67]], testada em `services/recomendacao.test.js`) e rota `POST /api/orcamentos/:id/recomendar`; a tela de aceite recalcula com debounce ao mudar eletricista, data ou início (06/11/2026).
**Regras:** [[P4.2 - Aceitar ou recusar orçamento]]

> Origem: pedido do professor na apresentação de 28/10/2026.
