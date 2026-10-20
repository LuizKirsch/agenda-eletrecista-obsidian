---
tags: [modulo]
entrega: 1
---
# Atividade

Mantém o catálogo de tipos de atividade usado nas Ordens de Serviço e nos orçamentos (ex.: troca de disjuntor, instalação de chuveiro), cada um com nome, duração padrão e valor padrão. Permite cadastrar novos tipos, ajustar nome, duração e valor e desativar tipos que não são mais usados; tipos nunca são excluídos, preservando o histórico das OS e dos orçamentos. A duração padrão sugere o horário de fim de cada atividade, e o valor padrão sugere o valor do item de serviço no orçamento.

## Entidades
- [[Tipo de Atividade]]
- [[Atividade da OS]]

## Processos e regras de negócio
- [[P5.1 - Gerenciar tipos de atividade]]

## Requisitos funcionais (8)
- [[RF 5.1]] (Alta) — O sistema deve manter um catálogo de tipos de atividade, cada um com nome, duração padrão e valor padrão, util…
- [[RF 5.2]] (Alta) — o sistema deve permitir cadastrar um tipo de atividade informando nome, duração padrão, entre 5 e 720 minutos,…
- [[RF 5.3]] (Alta) — o sistema deve permitir editar o nome, a duração padrão e o valor padrão de um tipo de atividade; a alteração…
- [[RF 5.4]] (Média) — o sistema não deve permitir dois tipos de atividade com o mesmo nome, sem diferenciar maiúsculas de minúsculas
- [[RF 5.5]] (Média) — o sistema deve permitir desativar e reativar um tipo de atividade; tipos inativos não devem ser oferecidos na…
- [[RF 5.6]] (Média) — o sistema não deve permitir excluir tipos de atividade; um tipo que não é mais usado deve ser desativado (RF 5…
- [[RF 5.7]] (Média) — o sistema deve exibir, para cada tipo de atividade, a quantidade de atividades de OS e de itens de serviço de…
- [[RF 5.8]] (Média) — o sistema deve manter ao menos um tipo de atividade ativo; sem tipo ativo, a criação de OS deve direcionar o u…

Voltar: [[00 - Visão Geral]]
