---
tags: [entidade]
tabela: orcamento_versao
---
# Versão do Orçamento

Armazena as versões anteriores de um orçamento.

**Tabela:** `orcamento_versao`
**Módulos:** [[Orçamento (módulo)|Orçamento]]

> Cada edição salva de um orçamento pendente gera uma versão numerada; as versões anteriores são consultadas só para leitura ([[RF 4.20]]). A versão guarda o estado *anterior* à edição, então a versão atual é a do próprio [[Orçamento]] (última versão + 1), e orçamentos antigos não precisaram de carga inicial.

## Relacionamentos
- N versões → 1 [[Orçamento]]
- N versões → 0..1 [[Usuário]] (autor da edição)

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `orcamento_id` | Orçamento versionado | BIGINT Unsigned | 20 | FK orcamento, NOT NULL, ON DELETE CASCADE |
| `numero` | Número da versão, de 1 a N por orçamento | INT |  | NOT NULL; UNIQUE com `orcamento_id` |
| `usuario_id` | Quem salvou a edição | BIGINT Unsigned | 20 | FK usuario, NULL, ON DELETE SET NULL |
| `snapshot` | Orçamento com cliente, endereço, itens e total, em JSON | TEXT |  | NOT NULL |
| `criado_em` | Data e hora da edição | DATETIME |  | NOT NULL, padrão CURRENT_TIMESTAMP |

## Implementação
- Migration: `migrations/20261106000400-create-orcamento-versao.js` · Model: `OrcamentoVersao` em `models/index.js` · Regras em `services/orcamento.service.js` (`atualizar`, `listarVersoes`, `detalharVersao`)
- Índice único `uq_orcamento_versao_numero` (`orcamento_id`, `numero`).
- O `snapshot` é a saída de `detalhar` (a mesma da API), não uma cópia das tabelas: mudar o formato da API muda o formato das versões novas.
- Rotas: `GET /api/orcamentos/:id/versoes` e `GET /api/orcamentos/:id/versoes/:numero`.
- Orçamento aceito ou recusado não é editado, então não gera versão.
- Ainda não há RN para a versão (o [[RF 4.20]] deixa as regras para um segundo momento).

> Fonte: decisão do projeto (pedido do professor, 28/10/2026); implementado em 06/11/2026.
