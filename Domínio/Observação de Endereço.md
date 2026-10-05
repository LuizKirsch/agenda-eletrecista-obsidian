---
tags: [entidade]
tabela: endereco_observacao
---
# Observação de Endereço

Armazena as observações registradas para cada endereço.

**Tabela:** `endereco_observacao`
**Módulos:** [[Cliente e Endereço]]

> Cada observação guarda a data de registro, formando o histórico do imóvel ([[RF 3.5]], [[RF 3.6]], [[RF 3.7]]).

## Relacionamentos
- N observações → 1 [[Endereço]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `endereco_id` | Endereço ao qual a observação pertence | BIGINT Unsigned | 20 | FK endereco, NOT NULL, ON DELETE CASCADE |
| `texto` | Conteúdo da observação | TEXT |  | NOT NULL |
| `criado_em` | Data e hora de registro da observação | DATETIME |  | NOT NULL, padrão CURRENT_TIMESTAMP |

> Fonte: Documentação Técnica V6, seção 15.
