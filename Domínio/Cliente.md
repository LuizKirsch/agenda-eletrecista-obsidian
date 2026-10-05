---
tags: [entidade]
tabela: cliente
---
# Cliente

Armazena os clientes atendidos.

**Tabela:** `cliente`
**Módulos:** [[Cliente e Endereço]], [[Agenda]]

> Cadastro mínimo, com apenas nome e telefone obrigatórios ([[RF 3.1]], [[RF 3.2]]). O telefone é único e só pode ser excluído o cliente sem OS vinculada ([[RF 3.11]]).

## Relacionamentos
- 1 cliente → N [[Endereço]]
- 1 cliente → N [[Ordem de Serviço]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `nome` | Nome do cliente (pessoa ou empresa) | VARCHAR | 120 | NOT NULL |
| `telefone` | Telefone de contato | VARCHAR | 20 | NOT NULL, UNIQUE; DDD e 8 ou 9 dígitos |
| `criado_em` | Data e hora do cadastro | DATETIME |  | NOT NULL, padrão CURRENT_TIMESTAMP |

> Fonte: Documentação Técnica V6, seção 15.
