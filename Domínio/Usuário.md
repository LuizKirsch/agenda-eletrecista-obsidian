---
tags: [entidade]
tabela: usuario
---
# Usuário

Armazena os usuários com acesso ao sistema.

**Tabela:** `usuario`
**Módulos:** [[Usuários e Acesso]]

> Dois perfis: eletricista e secretária. O perfil identifica o usuário e restringe apenas o cadastro, a edição e a exclusão de usuários, exclusivos da secretária ([[RF 2.2]], [[RF 2.3]], [[RF 2.9]], [[RF 2.10]], [[RF 2.11]]). A secretária inicial é criada pela migration da tabela ([[RF 2.13]]).

## Relacionamentos
- —

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `nome` | Nome do usuário | VARCHAR | 100 | NOT NULL |
| `login` | Login de acesso | VARCHAR | 60 | NOT NULL, UNIQUE |
| `senha_hash` | Senha criptografada (hash) | VARCHAR | 255 | NOT NULL |
| `perfil` | Perfil do usuário | ENUM |  | 'eletricista', 'secretaria'; NOT NULL |
| `ativo` | Indica se o usuário pode acessar o sistema | BOOLEAN |  | NOT NULL, padrão TRUE |

## Implementação
- Migration: `migrations/20260927000000-create-usuario.js` · Model: `Usuario` em `models/index.js`
- Conforme o dicionário. A migration falha se faltar `SECRETARIA_NOME`, `SECRETARIA_LOGIN` ou `SECRETARIA_SENHA` ([[RF 2.13]]).
- Hash bcrypt com custo 10; `senha_hash` nunca sai da API (o service devolve só `id, nome, login, perfil, ativo`).
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
