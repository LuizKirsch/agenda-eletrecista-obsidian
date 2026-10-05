---
tags: [entidade]
tabela: atividade_os
---
# Atividade da OS

Armazena as atividades agendadas de cada OS.

**Tabela:** `atividade_os`
**Módulos:** [[Ordem de Serviço (módulo)|Ordem de Serviço]], [[Agenda]], [[Atividade]]

> Cada atividade tem data, horário e status próprios ([[RF 6.3]], [[RF 1.6]]). A sequência é renumerada de 1 a N ao incluir ou remover atividades ([[P6.4 - Editar OS inteira#RN 35|RN 35]]).

## Relacionamentos
- N atividades → 1 [[Ordem de Serviço]]
- N atividades → 1 [[Tipo de Atividade]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `ordem_servico_id` | OS à qual pertence | BIGINT Unsigned | 20 | FK ordem_servico, NOT NULL |
| `tipo_atividade_id` | Tipo da atividade | BIGINT Unsigned | 20 | FK tipo_atividade, NOT NULL, ON DELETE RESTRICT |
| `sequencia` | Posição da atividade na OS | INT |  | NOT NULL |
| `data` | Data da atividade | DATE |  | NOT NULL |
| `hora_inicio` | Horário de início | TIME |  | NOT NULL |
| `hora_fim` | Horário de fim | TIME |  | NOT NULL, > hora_inicio |
| `status` | Situação da atividade | ENUM |  | 'agendada', 'concluida', 'cancelada'; padrão 'agendada' |

## Implementação
- Migration: `migrations/20260930000002-create-atividade-os.js` · Model: `AtividadeOs` em `models/index.js`
- CHECK `chk_atividade_os_horario` (`hora_fim > hora_inicio`) e índice `idx_atividade_os_data`.
- `status` tem DEFAULT `agendada`, mas aceita NULL.
- FK `ordem_servico_id` sem cascata; a renumeração da sequência é feita em `os.service` ([[P6.4 - Editar OS inteira#RN 35|RN 35]]).
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
