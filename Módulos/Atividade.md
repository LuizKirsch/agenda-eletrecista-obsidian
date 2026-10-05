---
tags: [modulo]
entrega: 1
---
# Atividade

Mantém o catálogo de tipos de atividade usado pela Agenda (ex.: troca de disjuntor, instalação de chuveiro), cada um com nome e duração padrão. Permite cadastrar novos tipos, ajustar nome e duração, desativar tipos que não são mais usados e excluir os que nunca foram vinculados a uma OS, preservando o histórico das OS já registradas. A duração padrão é usada pela Agenda para sugerir o horário de fim de cada atividade.

## Entidades
- [[Tipo de Atividade]]
- [[Atividade da OS]]

## Processos e regras de negócio
- [[P5.1 - Gerenciar tipos de atividade]]

## Requisitos funcionais (8)
- [[RF 5.1]] (Alta) — O sistema deve manter um catálogo de tipos de atividade, cada um com nome e duração padrão, utilizado na criaç…
- [[RF 5.2]] (Alta) — o sistema deve permitir cadastrar um tipo de atividade informando nome e duração padrão, entre 5 e 720 minutos…
- [[RF 5.3]] (Alta) — o sistema deve permitir editar o nome e a duração padrão de um tipo de atividade; a alteração da duração não d…
- [[RF 5.4]] (Média) — o sistema não deve permitir dois tipos de atividade com o mesmo nome, sem diferenciar maiúsculas de minúsculas…
- [[RF 5.5]] (Média) — o sistema deve permitir desativar e reativar um tipo de atividade; tipos inativos não devem ser oferecidos na…
- [[RF 5.6]] (Média) — o sistema deve permitir excluir um tipo de atividade somente se ele não estiver vinculado a nenhuma atividade…
- [[RF 5.7]] (Média) — o sistema deve exibir, para cada tipo de atividade, a quantidade de atividades de OS que o utilizam
- [[RF 5.8]] (Média) — o sistema deve manter ao menos um tipo de atividade ativo; sem tipo ativo, a criação de OS deve direcionar o u…

Voltar: [[00 - Visão Geral]]
