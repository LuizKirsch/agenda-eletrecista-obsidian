---
tags: [modulo]
entrega: 2
---
# Orçamento (módulo)

Montagem de orçamentos com itens de serviço, que são as atividades vinculadas ao orçamento: criados a partir do catálogo de tipos de atividade, com valor e tempo sugeridos e editáveis no orçamento, ou avulsos, para casos fora do catálogo. Cada item tem quantidade, valor unitário e tempo, e o total é calculado. O orçamento é opcional, exige cliente e endereço, pode ser editado ou excluído enquanto pendente, tem status pendente, aceito ou recusado e, ao ser aceito, gera uma OS com uma atividade por item.

## Entidades
- [[Orçamento]]
- [[Item de Serviço]]
- [[Tipo de Atividade]] (catálogo, com valor padrão)
- [[Ordem de Serviço]]

Modelo de dados: [[Proposta - Modelo do Orçamento]]

## Processos e regras de negócio
- [[P4.1 - Montar orçamento]]
- [[P4.2 - Aceitar ou recusar orçamento]]
- [[P4.3 - Editar e excluir orçamento]]

## Requisitos funcionais (16)
- [[RF 4.1]] (Média) — o sistema deve permitir informar um valor padrão em cada tipo de atividade, usado como valor sugerido do item…
- [[RF 4.2]] (Média) — o catálogo de tipos de atividade deve ser reutilizável em múltiplos orçamentos; somente tipos ativos podem ser…
- [[RF 4.3]] (Média) — o sistema deve permitir alterar o valor de um item apenas dentro de um orçamento específico
- [[RF 4.4]] (Média) — a alteração de valor não deve alterar o valor padrão do catálogo geral
- [[RF 4.5]] (Média) — o sistema deve permitir criar item avulso (nome, valor e tempo livres) vinculado a um orçamento específico (al…
- [[RF 4.6]] (Média) — o item avulso não deve ser salvo automaticamente no catálogo geral
- [[RF 4.7]] (Média) — a OS gerada pelo aceite de um orçamento ([[RF 4.13]]) fica vinculada a ele; o orçamento é opcional, cada OS te…
- [[RF 4.8]] (Alta) — o sistema deve permitir criar um orçamento informando cliente, endereço, observações e um ou mais itens de ser…
- [[RF 4.9]] (Alta) — cada item de serviço deve possuir descrição, quantidade, valor unitário e tempo; ao escolher um tipo de ativid…
- [[RF 4.10]] (Média) — o sistema deve exibir o total do orçamento, calculado pela soma da quantidade multiplicada pelo valor unitário…
- [[RF 4.11]] (Alta) — o orçamento deve possuir status pendente, aceito ou recusado; todo orçamento é criado como pendente
- [[RF 4.12]] (Média) — o sistema deve permitir aceitar ou recusar um orçamento pendente; orçamentos aceitos ou recusados não mudam ma…
- [[RF 4.13]] (Alta) — ao aceitar um orçamento, o sistema deve gerar uma OS com o cliente e o endereço do orçamento e uma atividade a…
- [[RF 4.14]] (Média) — o sistema deve listar os orçamentos com cliente, data de criação, status e total, do mais recente para o mais antig…
- [[RF 4.15]] (Média) — o sistema deve permitir editar e excluir, com confirmação, somente o orçamento pendente; o orçamento aceito ou…
- [[RF 4.16]] (Média) — ao fechar o formulário de orçamento depois de qualquer informação preenchida, por qualquer meio (Cancelar, Fechar, clique fora…

Voltar: [[00 - Visão Geral]]
