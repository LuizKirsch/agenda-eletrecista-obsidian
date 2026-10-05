---
tags: [requisito]
id: "RF 1.14"
modulo: "[[Agenda]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 1.14

ao arrastar uma atividade de uma OS que possua mais de uma atividade agendada, o sistema deve perguntar se a remarcação vale para a OS inteira ou apenas para a atividade arrastada, permitindo também cancelar o arraste; na opção OS inteira, a atividade arrastada vai para o dia e horário onde foi solta e as demais atividades agendadas da OS vão para o mesmo dia, encadeadas na ordem da sequência e mantendo a duração de cada uma (as anteriores logo antes e as posteriores logo depois, sem intervalos entre elas); concluídas e canceladas não mudam; se o encadeamento não couber no dia, nada é alterado e o usuário é avisado; em OS com uma única atividade agendada, a remarcação é aplicada sem perguntar (alterado: decisão do projeto);

**Módulo:** [[Agenda]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]], [[Usuário]]

> Fonte: Documentação Técnica V6, seção 4.
