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
- 1 eletricista → N [[Ordem de Serviço]] (responsável, [[RF 6.21]])
- 1 eletricista → N [[Atividade da OS]] ([[RF 6.22]]); com atividades vinculadas, não pode ser excluído ([[RF 2.14]])

## Dicionário de dados
| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `nome` | Nome do usuário | VARCHAR | 100 | NOT NULL |
| `login` | Login de acesso | VARCHAR | 60 | NOT NULL, UNIQUE |
| `senha_hash` | Senha criptografada (hash) | VARCHAR | 255 | NOT NULL |
| `perfil` | Perfil do usuário | ENUM |  | 'eletricista', 'secretaria'; NOT NULL |
| `ativo` | Indica se o usuário pode acessar o sistema | BOOLEAN |  | NOT NULL, padrão TRUE |
| `cor` | Cor do eletricista na agenda ([[RF 1.13]], [[RF 1.14]]) | VARCHAR | 7 | NULL; formato `#rrggbb`; sempre NULL para a secretária |

## Implementação
- Migration: `migrations/20260927000000-create-usuario.js` · Model: `Usuario` em `models/index.js`
- Conforme o dicionário. A migration falha se faltar `SECRETARIA_NOME`, `SECRETARIA_LOGIN` ou `SECRETARIA_SENHA` ([[RF 2.13]]).
- `POST`, `PUT` e `DELETE /api/usuarios` usam `somenteSecretaria` ([[RF 2.9]], 06/11/2026).
- Eletricista com OS ou atividades não é excluído: o service devolve 409 e as FKs `eletricista_id` são `RESTRICT` ([[RF 2.14]]). Trocar o perfil de um eletricista com vínculos não é bloqueado.
- `cor` entrou em `migrations/20261106000500-add-usuario-cor.js`; os eletricistas existentes receberam a paleta em ordem de id. A paleta de 10 cores fica em `config/paleta.js` e é duplicada em `client/src/paleta.js`. O service valida o formato (400) e, para eletricista sem cor, atribui a primeira cor da paleta ainda não usada (06/11/2026).
- Hash bcrypt com custo 10; `senha_hash` nunca sai da API (o service devolve só `id, nome, login, perfil, ativo`).
- Divergências: [[Status da Implementação]]

> Fonte: Documentação Técnica V6, seção 15.
