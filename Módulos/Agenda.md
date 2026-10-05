---
tags: [modulo]
entrega: 1
---
# Agenda

Exibe as Ordens de Serviço em uma visão semanal (segunda a domingo, das 00h00 às 23h59) e concentra a interação com elas na tela: navegar entre semanas, iniciar uma OS a partir de um horário livre, arrastar atividades para remarcar e abrir o detalhe da OS ao selecionar um bloco. As regras da OS (criação, edição, remarcação, conflito, status e exclusão) ficam no módulo [[Ordem de Serviço (módulo)|Ordem de Serviço]]; a Agenda aciona essas regras e reflete o resultado imediatamente.

## Entidades
Nenhuma própria: exibe e move as [[Atividade da OS|atividades]] das [[Ordem de Serviço|Ordens de Serviço]].

## Processos e regras de negócio
- [[P1.1 - Arrastar atividade]]

## Requisitos funcionais (12)
- [[RF 1.1]] (Alta) — O sistema deve exibir a agenda em visão semanal, de segunda a domingo, em período integral (das 00h00 às 23h59…
- [[RF 1.2]] (Alta) — o sistema deve permitir navegar para a semana anterior e para a próxima, e retornar à semana atual
- [[RF 1.3]] (Média) — o sistema deve destacar o dia atual na visão semanal
- [[RF 1.4]] (Média) — o sistema deve permitir iniciar a criação de uma OS clicando em um horário livre da agenda, com data e hora de…
- [[RF 1.5]] (Alta) — o sistema deve permitir acessar o gerenciamento de tipos de atividade (módulo Atividade) por um botão no cabeç…
- [[RF 1.6]] (Alta) — o sistema deve indicar o status de cada atividade (agendada, concluída, cancelada), com distinção visual na ag…
- [[RF 1.7]] (Média) — em uma OS com mais de uma atividade, cada bloco da agenda deve indicar sua posição na OS (ex.: 1/2 · OS 2)
- [[RF 1.8]] (Média) — atividades com horários sobrepostos devem ser exibidas lado a lado na agenda, considerando também a altura mín…
- [[RF 1.9]] (Alta) — o sistema deve permitir remarcar arrastando uma atividade para outro dia/horário, com encaixe em intervalos de…
- [[RF 1.10]] (Alta) — ao arrastar uma atividade de uma OS que possua mais de uma atividade agendada, o sistema deve perguntar se a r…
- [[RF 1.11]] (Alta) — ao selecionar um bloco (atividade ou grupo), o sistema deve abrir o detalhe da OS (RF 6.19) com a atividade se…
- [[RF 1.12]] (Média) — as alterações realizadas na agenda devem refletir imediatamente na visão semanal

> Separada do módulo Ordem de Serviço na V7. Ver [[Proposta - Módulo Ordem de Serviço]].

Voltar: [[00 - Visão Geral]]
