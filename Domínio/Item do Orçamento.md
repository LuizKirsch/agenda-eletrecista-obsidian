---
tags: [entidade]
tabela: orcamento_item
---
# Item do Orçamento

Armazena as atividades de cada orçamento, do catálogo ou avulsas.

**Tabela:** `orcamento_item`
**Módulos:** [[Orçamento (módulo)|Orçamento]]

> Atividade do catálogo: `tipo_atividade_id` preenchido; o nome e o `valor_padrao` do [[Tipo de Atividade]] são copiados para `descricao` e `valor_unitario`, e o valor pode ser editado sem alterar o catálogo ([[RF 4.3]], [[RF 4.4]]). Atividade avulsa: `tipo_atividade_id` NULL, nome e valor livres, nunca salva no catálogo ([[RF 4.5]], [[RF 4.6]]). Ver [[Proposta - Modelo do Orçamento]].

## Relacionamentos
- N itens → 1 [[Orçamento]]
- N itens → 0..1 [[Tipo de Atividade]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `orcamento_id` | Orçamento ao qual pertence | BIGINT Unsigned | 20 | FK orcamento, NOT NULL, ON DELETE CASCADE |
| `tipo_atividade_id` | Atividade do catálogo (NULL = avulsa) | BIGINT Unsigned | 20 | FK tipo_atividade, NULL, ON DELETE RESTRICT |
| `descricao` | Nome da atividade no orçamento | VARCHAR | 100 | NOT NULL |
| `quantidade` | Quantidade | INT |  | NOT NULL, padrão 1, > 0 |
| `valor_unitario` | Valor cobrado neste orçamento | DECIMAL | 10,2 | NOT NULL, ≥ 0 |
| `sequencia` | Posição do item no orçamento | INT |  | NOT NULL |

## Implementação
- Pendente (entrega 2).
