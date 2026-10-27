---
tags: [entidade]
tabela: orcamento
---
# Orçamento

Armazena os orçamentos de um cliente.

**Tabela:** `orcamento`
**Módulos:** [[Orçamento (módulo)|Orçamento]], [[Ordem de Serviço (módulo)|Ordem de Serviço]]

> Montado com atividades do catálogo de [[Tipo de Atividade]] (valor editável só dentro do orçamento) e com atividades avulsas. É opcional e pode ser vinculado a uma [[Ordem de Serviço]] ([[RF 4.7]]). O total não é armazenado: é a soma de `quantidade × valor_unitario` dos itens. Ver [[Proposta - Modelo do Orçamento]].

## Relacionamentos
- N orçamentos → 1 [[Cliente]]
- N orçamentos → 1 [[Endereço]]
- 1 orçamento → N [[Item de Serviço]]
- 0..1 orçamento ↔ 0..1 [[Ordem de Serviço]] ([[RF 4.7]])

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `cliente_id` | Cliente do orçamento | BIGINT Unsigned | 20 | FK cliente, NOT NULL, ON DELETE RESTRICT |
| `endereco_id` | Endereço do serviço | BIGINT Unsigned | 20 | FK endereco, NOT NULL, ON DELETE RESTRICT |
| `ordem_servico_id` | OS vinculada | BIGINT Unsigned | 20 | FK ordem_servico, NULL, UNIQUE |
| `status` | Situação do orçamento | ENUM |  | 'pendente', 'aceito', 'recusado'; padrão 'pendente' |
| `observacao` | Observações livres | TEXT |  |  |
| `criado_em` | Data de criação | DATETIME |  | NOT NULL |

## Implementação
- Migration: `migrations/20261027000001-create-orcamento.js` · Model: `Orcamento` em `models/index.js` · Regras em `services/orcamento.service.js`
- `ordem_servico_id` com `ON DELETE SET NULL`: excluir a OS gerada desfaz só o vínculo, e o orçamento aceito continua como histórico (decisão de implementação, 27/10/2026).
- O vínculo com a OS é criado só pelo aceite ([[RF 4.13]]); não há tela para vincular um orçamento a uma OS já existente.
