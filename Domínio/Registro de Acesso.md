---
tags: [entidade, lgpd]
tabela: registro_acesso
---
# Registro de Acesso

Armazena os logins realizados no sistema, por 6 meses.

**Tabela:** `registro_acesso`
**Módulos:** [[Usuários e Acesso]]

> Guarda usuário, IP e data e hora de cada login com sucesso ([[RF 2.14]]); registros com mais de 6 meses são apagados automaticamente ([[RF 2.15]]). O login é copiado no registro para manter a identificação se o usuário for excluído ([[RF 2.11]]).

## Relacionamentos
- N registros → 0..1 [[Usuário]]

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `usuario_id` | Usuário que fez o login | BIGINT Unsigned | 20 | FK usuario, ON DELETE SET NULL |
| `login` | Login usado no acesso | VARCHAR | 60 | NOT NULL |
| `ip` | Endereço IP de origem (IPv4 ou IPv6) | VARCHAR | 45 | NOT NULL |
| `acessado_em` | Data e hora do login | DATETIME |  | NOT NULL, padrão CURRENT_TIMESTAMP |

## Implementação
- Ainda não existe (pendente).

> Origem: ajuste de LGPD [[L5 - Registro de acessos|L5]].
