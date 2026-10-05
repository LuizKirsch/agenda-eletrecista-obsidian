---
tags: [entidade]
tabela: ordem_servico
---
# Ordem de Serviço

Armazena as Ordens de Serviço (OS).

**Tabela:** `ordem_servico`
**Módulos:** [[Agenda]], [[Orçamento (módulo)|Orçamento]]

> Agrupa uma ou mais atividades de um mesmo cliente/endereço ([[RF 1.4]]). Cliente e endereço são obrigatórios, e as chaves impedem excluir cliente ou endereço com OS vinculada ([[RF 3.11]]).

## Relacionamentos
- N OS → 1 [[Cliente]]
- N OS → 1 [[Endereço]]
- 1 OS → N [[Atividade da OS]]
- 0..1 [[Orçamento]] vinculado (RF 4.7)

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `cliente_id` | Cliente da OS | BIGINT Unsigned | 20 | FK cliente, NOT NULL, ON DELETE RESTRICT |
| `endereco_id` | Endereço do atendimento | BIGINT Unsigned | 20 | FK endereco, NOT NULL, ON DELETE RESTRICT |
| `observacao` | Observações livres da OS | TEXT |  |  |

## Implementação
- Migration: `migrations/20260930000001-create-ordem-servico.js` · Model: `OrdemServico` em `models/index.js`
- ⚠️ `endereco_id` **aceita NULL** ([[RF 1.4]]).
- FKs sem `ON DELETE` explícito (o padrão do banco já impede excluir cliente/endereço com OS). Ao excluir a OS, o service apaga as atividades antes.
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
