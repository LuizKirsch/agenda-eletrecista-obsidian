---
tags: [arquitetura]
---
# API REST

Todas as rotas ficam sob `/api` e, exceto `POST /auth/login`, exigem sessão válida (middleware `autenticar`). `GET /health`, fora de `/api`, responde `{ "status": "ok" }`.

## Convenções
- **Sessão:** cookie `token` (JWT com `{ id }`), `httpOnly`, `sameSite=lax` e `secure` em produção, com validade de `JWT_EXPIRES_IN` (padrão 7d). A cada requisição o usuário é recarregado do banco; usuário inativo ou removido recebe 401 ([[P2.1 - Autenticar#RN 23|RN 23]]).
- **Erros:** sempre `{ "erro": "mensagem" }`. Erros criados com `httpErro(status, msg)` têm a mensagem exibida ao usuário; os demais viram 500 com "Não foi possível concluir a operação. Tente novamente." e são logados no console.
- **Validação:** feita nos controllers (`lerCampos`, `exigirCampos`, `lerHorario`, `lerOs`), e as regras de negócio ficam nos services.
- **Datas e horas:** `YYYY-MM-DD` e `HH:MM` como texto ([[Decisão - Datas e Horas como Texto]]).
- **Conflito:** as operações que gravam horário devolvem `aviso_conflito: true|false` e não bloqueiam o salvamento ([[P1.5 - Verificar conflito de horário#RN 11|RN 11]]).
- Status usados: 400 (validação), 401 (sessão), 403 (perfil), 404, 409 (regra de negócio), 201 (criação) e 204 (sem corpo).

## Auth
| Método | Rota | Descrição |
| --- | --- | --- |
| POST | `/auth/login` | `{ login, senha }` → usuário; grava o cookie. Falha: 401 "Login ou senha inválidos." ([[RF 2.4]]) |
| POST | `/auth/logout` | Limpa o cookie ([[RF 2.6]]) |
| GET | `/auth/me` | Usuário da sessão `{ id, nome, perfil }` ([[RF 2.7]]) |

## Usuários
| Método | Rota | Perfil | Descrição |
| --- | --- | --- | --- |
| GET | `/usuarios` | ambos | Lista `id, nome, login, perfil, ativo`, por nome ([[RF 2.8]]) |
| POST | `/usuarios` | ambos ⚠️ | Cadastra; deveria ser só secretária ([[RF 2.9]]) |
| PUT | `/usuarios/:id` | secretária | Edita; senha vazia mantém a atual; bloqueia mudar o próprio perfil ou se desativar ([[RF 2.10]], [[RF 2.12]]) |
| DELETE | `/usuarios/:id` | secretária | Exclui; não permite excluir o próprio usuário ([[RF 2.11]]) |

## Clientes e endereços
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/clientes?busca=` | Lista por nome; `busca` com `LIKE` em nome ou telefone ([[RF 3.8]]) |
| POST | `/clientes` | `{ nome, telefone }` ([[RF 3.1]]) |
| GET | `/clientes/:id` | Cliente com endereços |
| POST | `/clientes/:id/enderecos` | Novo endereço ([[RF 3.3]]) |
| GET | `/enderecos/:id` | Endereço com cliente |
| GET | `/enderecos/:id/observacoes` | Observações, da mais recente para a mais antiga ([[RF 3.7]]) |
| POST | `/enderecos/:id/observacoes` | `{ texto }` ([[RF 3.5]]) |

Edição e exclusão ([[RF 3.9]] a [[RF 3.12]]) ainda não têm rotas.

## Tipos de atividade
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/tipos-atividade?ativos=1` | Lista com `uso` (quantidade de atividades) ([[RF 5.7]]); `ativos=1` filtra os ativos |
| POST | `/tipos-atividade` | `{ nome, duracao_padrao_min }` (5–720) ([[RF 5.2]]); nome repetido → 409 ([[RF 5.4]]) |
| PUT | `/tipos-atividade/:id` | Edita nome e duração ([[RF 5.3]]) |
| PATCH | `/tipos-atividade/:id/situacao` | `{ ativo }`; recusa desativar o último ativo ([[RF 5.5]], [[RF 5.8]]) |
| DELETE | `/tipos-atividade/:id` | Só sem uso; recusa excluir o último ativo ([[RF 5.6]]) |

## Agenda e OS
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/agenda?inicio=&fim=` | Atividades do período com `os_id`, `sequencia`, `total`, `tipo`, `status`, `conflito`, cliente e endereço ([[RF 1.1]], [[RF 1.12]], [[RF 1.18]]) |
| POST | `/os` | `{ cliente_id, endereco_id, observacao, atividades[] }` → `{ id, aviso_conflito }` ([[P1.1 - Criar OS]]) |
| GET | `/os/:id` | OS com cliente, endereço e atividades (com `conflito`) ([[RF 1.22]]) |
| PUT | `/os/:id` | Substitui dados e atividades; linhas com `id` são mantidas, as sem `id` são criadas e as ausentes, removidas; renumera a sequência ([[P1.4 - Editar OS inteira]]) |
| DELETE | `/os/:id` | Exclui a OS e as atividades ([[RF 1.26]]) |
| POST | `/os/:id/deslocar` | `{ atividade_id, data, hora_inicio }`: encadeia as agendadas no dia; 409 se não couber ([[P1.2 - Remarcar OS por arraste#RN 6\|RN 6]]) |
| POST | `/os/:id/concluir` | Agendadas → concluídas ([[RF 1.24]]) |
| PATCH | `/atividades-os/:id/horario` | `{ data, hora_inicio, hora_fim }`, só agendada ([[P1.3 - Remarcar atividade]]) |
| PATCH | `/atividades-os/:id/status` | `{ status: 'concluida' \| 'cancelada' }`, só agendada ([[RF 1.23]]) |
| DELETE | `/atividades-os/:id` | Só concluída/cancelada; se for a última, exclui a OS; senão renumera ([[P1.7 - Excluir]]) |

## Regra de conflito
Fica em um único lugar, `agenda.service.idsEmConflito`: há conflito entre atividades não canceladas, na mesma data, com intervalos sobrepostos. Atividades encostadas (o fim de uma igual ao início da outra) não conflitam.

Ver: [[Stack e Ambiente]], [[Frontend]]
