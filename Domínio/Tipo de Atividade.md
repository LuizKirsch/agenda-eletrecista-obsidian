---
tags: [entidade]
tabela: tipo_atividade
---
# Tipo de Atividade

Armazena o catálogo de tipos de atividade e sua duração padrão.

**Tabela:** `tipo_atividade`
**Módulos:** [[Atividade]], [[Ordem de Serviço (módulo)|Ordem de Serviço]]

> Mantida pelo módulo Atividade e usada na Ordem de Serviço para sugerir o horário de fim das atividades ([[RF 6.4]], [[RF 5.1]] a [[RF 5.8]]). A coluna nome usa a collation utf8mb4_0900_as_ci, que não diferencia maiúsculas de minúsculas, mas diferencia acentos ([[RF 5.4]]).

## Relacionamentos
- 1 tipo → N [[Atividade da OS]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `nome` | Nome do tipo de atividade | VARCHAR | 100 | NOT NULL, UNIQUE |
| `duracao_padrao_min` | Duração padrão em minutos | INT |  | NOT NULL, entre 5 e 720 |
| `ativo` | Indica se o tipo pode ser usado em novas atividades | BOOLEAN |  | NOT NULL, padrão TRUE |

## Implementação
- Migration: `migrations/20260929000001-create-tipo-atividade.js` · Model: `TipoAtividade` em `models/index.js`
- CHECK `chk_tipo_atividade_duracao` (5 a 720).
- No SQLite, a coluna `nome` usa `COLLATE NOCASE` ([[Decisão - SQLite em Desenvolvimento]]).
- O uso (`uso`) é contado em `tipoAtividade.service.contarUso` ([[RF 5.7]]).
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
