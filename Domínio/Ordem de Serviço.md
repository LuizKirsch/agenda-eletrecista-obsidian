---
tags: [entidade]
tabela: ordem_servico
---
# Ordem de Serviço

Armazena as Ordens de Serviço (OS).

**Tabela:** `ordem_servico`
**Módulos:** [[Ordem de Serviço (módulo)|Ordem de Serviço]], [[Agenda]], [[Orçamento (módulo)|Orçamento]]

> Agrupa uma ou mais atividades de um mesmo cliente/endereço ([[RF 6.1]]). Cliente e endereço são obrigatórios ([[P6.1 - Criar OS#RN 34|RN 34]]); as chaves impedem excluir cliente ou endereço com OS vinculada ([[RF 3.11]]).

## Relacionamentos
- N OS → 1 [[Cliente]]
- N OS → 1 [[Endereço]]
- N OS → 1 [[Usuário]] (eletricista responsável, [[RF 6.21]])
- 1 OS → N [[Atividade da OS]]
- 0..1 [[Orçamento]] vinculado (RF 4.7)

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `cliente_id` | Cliente da OS | BIGINT Unsigned | 20 | FK cliente, NOT NULL, ON DELETE RESTRICT |
| `endereco_id` | Endereço do atendimento | BIGINT Unsigned | 20 | FK endereco, NOT NULL, ON DELETE RESTRICT |
| `eletricista_id` | Eletricista responsável ([[RF 6.21]]) | BIGINT Unsigned | 20 | FK usuario (perfil eletricista), NOT NULL, ON DELETE RESTRICT |
| `observacao` | Observação da OS (uma por OS) | TEXT |  |  |

## Implementação
- Migration: `migrations/20260930000001-create-ordem-servico.js` · Model: `OrdemServico` em `models/index.js`
- FKs sem `ON DELETE` explícito (o padrão do banco já impede excluir cliente/endereço com OS). Ao excluir a OS, o service apaga as atividades antes.
- `eletricista_id` entrou em `migrations/20261106000100-add-eletricista-os-atividade.js`, FK `RESTRICT` (eletricista com OS não é excluído, [[RF 2.14]]). As OS que já existiam receberam o primeiro eletricista cadastrado, ativo de preferência.
- ⚠️ `eletricista_id` **sem NOT NULL** no banco; a API exige o responsável e recusa usuário inativo ou de outro perfil ([[RF 6.21]]).
- ⚠️ `endereco_id` **sem NOT NULL** no banco; desde 06/11/2026 a API exige o endereço e confere que é do cliente ([[RF 6.1]]). Nenhuma OS do `dev.sqlite` está sem endereço.
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
