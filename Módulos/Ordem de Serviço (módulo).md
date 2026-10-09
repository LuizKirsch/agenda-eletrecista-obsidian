---
tags: [modulo]
entrega: 1
---
# Ordem de Serviço (módulo)

Mantém as Ordens de Serviço (OS) do eletricista e da secretária. Cada OS reúne cliente, endereço e observações e é composta por uma ou mais atividades, cada uma com tipo, data, horário e status próprios (agendada, concluída ou cancelada). O tipo e a duração sugerida de cada atividade vêm do catálogo mantido no módulo [[Atividade]]. O cliente é obrigatório e o endereço é opcional; os dois podem ser cadastrados sem sair da OS. O módulo permite criar e editar a OS, remarcar a OS inteira ou apenas uma atividade, concluir, cancelar e excluir, e sinaliza conflitos de horário sem bloquear o salvamento. A visualização e os gestos na tela ficam no módulo [[Agenda]].

## Entidades
- [[Ordem de Serviço]]
- [[Atividade da OS]]
- [[Tipo de Atividade]]
- [[Cliente]]
- [[Endereço]]

## Processos e regras de negócio
- [[P6.1 - Criar OS]]
- [[P6.2 - Remarcar OS inteira]]
- [[P6.3 - Remarcar atividade]]
- [[P6.4 - Editar OS inteira]]
- [[P6.5 - Verificar conflito de horário]]
- [[P6.6 - Concluir ou cancelar]]
- [[P6.7 - Excluir]]
- [[P6.8 - Adicionar atividade a OS existente]]

## Requisitos funcionais (19)
- [[RF 6.1]] (Alta) — o sistema deve permitir criar uma Ordem de Serviço (OS) informando cliente, endereço, observações e uma ou mai…
- [[RF 6.2]] (Alta) — na criação e na edição da OS, o sistema deve permitir buscar o cliente por parte do nome ou do telefone e, se…
- [[RF 6.3]] (Alta) — cada atividade da OS deve possuir tipo, data, horário de início, horário de fim e status próprios
- [[RF 6.4]] (Média) — ao escolher o tipo ou alterar o horário de início de uma atividade, o sistema deve calcular o horário de fim a…
- [[RF 6.5]] (Média) — ao adicionar uma nova atividade à OS, o sistema deve sugerir início no horário de fim da atividade anterior, n…
- [[RF 6.6]] (Alta) — o sistema deve impedir o salvamento de uma atividade cujo horário de fim não seja posterior ao de início
- [[RF 6.7]] (Média) — o sistema deve permitir adicionar uma atividade a uma OS existente pelas ações da OS inteira; a nova linha sug…
- [[RF 6.8]] (Alta) — o sistema deve permitir editar a OS inteira: cliente, endereço, observações e inclusão, remoção ou alteração d…
- [[RF 6.9]] (Alta) — o sistema deve permitir remarcar apenas uma atividade (data, início e fim), sem alterar as demais atividades,…
- [[RF 6.10]] (Alta) — na remarcação da OS inteira, a atividade de referência vai para o dia e horário escolhidos e as demais ativida…
- [[RF 6.11]] (Alta) — atividades concluídas ou canceladas não podem ser arrastadas, deslocadas pela remarcação da OS nem alteradas o…
- [[RF 6.12]] (Média) — o sistema deve sinalizar conflito quando uma atividade se sobrepuser a outra no mesmo dia, tanto na agenda qua…
- [[RF 6.13]] (Média) — o conflito de horário não deve impedir o salvamento: o usuário é avisado e decide se ajusta
- [[RF 6.14]] (Média) — atividades canceladas não devem ser consideradas na verificação de conflito
- [[RF 6.15]] (Alta) — o sistema deve permitir concluir ou cancelar uma atividade individualmente
- [[RF 6.16]] (Média) — o sistema deve permitir concluir a OS inteira, passando todas as suas atividades agendadas para concluídas
- [[RF 6.17]] (Média) — o sistema deve permitir excluir uma atividade concluída ou cancelada; ao excluir a última atividade, a OS tamb…
- [[RF 6.18]] (Média) — o sistema deve permitir excluir a OS inteira
- [[RF 6.19]] (Alta) — o detalhe da OS deve exibir cliente, telefone, endereço e observações da OS, a lista de todas as atividades da…

> Separado da Agenda na V7. Ver [[Proposta - Módulo Ordem de Serviço]].

Voltar: [[00 - Visão Geral]]
