---
tags: [entidade]
tabela: endereco
---
# Endereço

Armazena os endereços (imóveis) atendidos.

**Tabela:** `endereco`
**Módulos:** [[Cliente e Endereço]], [[Agenda]]

> Entidade própria vinculada ao cliente; um cliente pode ter N endereços ([[RF 3.3]], [[RF 3.4]]). As observações ficam em endereco_observacao.

## Relacionamentos
- N endereços → 1 [[Cliente]]
- 1 endereço → N [[Observação de Endereço]]
- 1 endereço → N [[Ordem de Serviço]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `cliente_id` | Cliente dono do endereço | BIGINT Unsigned | 20 | FK cliente, NOT NULL, ON DELETE CASCADE |
| `identificacao` | Apelido do endereço (ex.: casa, escritório) | VARCHAR | 60 |  |
| `logradouro` | Rua ou avenida | VARCHAR | 150 | NOT NULL |
| `numero` | Número do imóvel | VARCHAR | 10 |  |
| `complemento` | Complemento (apto, bloco, sala) | VARCHAR | 60 |  |
| `bairro` | Bairro | VARCHAR | 80 |  |
| `cidade` | Cidade | VARCHAR | 80 | NOT NULL |
| `ponto_referencia` | Ponto de referência para chegar ao local | VARCHAR | 150 |  |

## Implementação
- Migration: `migrations/20260928000002-create-endereco.js` · Model: `Endereco` em `models/index.js`
- ⚠️ FK `cliente_id` **sem ON DELETE CASCADE** ([[P3.3 - Editar e excluir cliente, endereço e observação#RN 43|RN 43]]).
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
