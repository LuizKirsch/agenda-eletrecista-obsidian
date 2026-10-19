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
- N orçamentos → 0..1 [[Endereço]]
- 1 orçamento → N [[Item do Orçamento]]
- 0..1 orçamento ↔ 0..1 [[Ordem de Serviço]] ([[RF 4.7]])

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `cliente_id` | Cliente do orçamento | BIGINT Unsigned | 20 | FK cliente, NOT NULL, ON DELETE RESTRICT |
| `endereco_id` | Endereço do serviço | BIGINT Unsigned | 20 | FK endereco, NULL, ON DELETE RESTRICT |
| `ordem_servico_id` | OS vinculada | BIGINT Unsigned | 20 | FK ordem_servico, NULL, UNIQUE |
| `status` | Situação do orçamento | ENUM |  | 'aberto', 'aprovado', 'recusado'; padrão 'aberto' |
| `observacao` | Observações livres | TEXT |  |  |
| `criado_em` | Data de criação | DATETIME |  | NOT NULL |

## Implementação
- Pendente (entrega 2).
