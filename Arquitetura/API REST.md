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
- **Conflito:** as operações que gravam horário devolvem `aviso_conflito: true|false` e não bloqueiam o salvamento ([[P6.5 - Verificar conflito de horário#RN 11|RN 11]]).
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
| PUT | `/clientes/:id` | `{ nome, telefone }` ([[RF 3.9]]) |
| DELETE | `/clientes/:id` | 409 se houver OS ou orçamento; senão exclui endereços, observações e o cliente ([[RF 3.11]]) |
| POST | `/clientes/:id/enderecos` | Novo endereço ([[RF 3.3]]) |
| GET | `/enderecos/:id` | Endereço com cliente |
| PUT | `/enderecos/:id` | Mesmos campos do cadastro; devolve o endereço com cliente ([[RF 3.10]]) |
| DELETE | `/enderecos/:id` | 409 se houver OS ou orçamento; senão exclui as observações e o endereço ([[RF 3.11]]) |
| GET | `/enderecos/:id/observacoes` | Observações, da mais recente para a mais antiga ([[RF 3.7]]) |
| POST | `/enderecos/:id/observacoes` | `{ texto }` ([[RF 3.5]]) |
| PUT | `/enderecos/:id/observacoes/:observacaoId` | `{ texto }`; mantém `criado_em` ([[RF 3.10]]) |
| DELETE | `/enderecos/:id/observacoes/:observacaoId` | Exclui a observação ([[RF 3.12]]) |

## Tipos de atividade
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/tipos-atividade?ativos=1` | Lista com `valor_padrao` e `uso` (atividades de OS + itens de orçamento) ([[RF 5.7]]); `ativos=1` filtra os ativos |
| POST | `/tipos-atividade` | `{ nome, duracao_padrao_min, valor_padrao }` (5–720; valor opcional, ≥ 0, 2 casas) ([[RF 5.2]]); nome repetido → 409 ([[RF 5.4]]) |
| PUT | `/tipos-atividade/:id` | Edita nome, duração e valor padrão ([[RF 5.3]]) |
| PATCH | `/tipos-atividade/:id/situacao` | `{ ativo }`; recusa desativar o último ativo ([[RF 5.5]], [[RF 5.8]]) |
| DELETE | `/tipos-atividade/:id` | Só sem uso; recusa excluir o último ativo ([[RF 5.6]]) |

## Agenda e OS
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/agenda?inicio=&fim=` | Atividades do período com `os_id`, `sequencia`, `total`, `tipo`, `status`, `conflito`, cliente e endereço ([[RF 1.1]], [[RF 1.7]], [[RF 6.12]]) |
| POST | `/os` | `{ cliente_id, endereco_id, observacao, atividades[] }` → `{ id, aviso_conflito }` ([[P6.1 - Criar OS]]) |
| GET | `/os/:id` | OS com cliente, endereço e atividades (com `conflito`) ([[RF 1.11]]) |
| PUT | `/os/:id` | Substitui dados e atividades; linhas com `id` são mantidas, as sem `id` são criadas e as ausentes, removidas; renumera a sequência ([[P6.4 - Editar OS inteira]]) |
| DELETE | `/os/:id` | Exclui a OS e as atividades ([[RF 6.18]]) |
| POST | `/os/:id/deslocar` | `{ atividade_id, data, hora_inicio }`: encadeia as agendadas no dia; 409 se não couber ([[P1.1 - Arrastar atividade#RN 6\|RN 6]]) |
| POST | `/os/:id/concluir` | Agendadas → concluídas ([[RF 6.16]]) |
| PATCH | `/atividades-os/:id/horario` | `{ data, hora_inicio, hora_fim }`, só agendada ([[P6.3 - Remarcar atividade]]) |
| PATCH | `/atividades-os/:id/status` | `{ status: 'concluida' \| 'cancelada' }`, só agendada ([[RF 6.15]]) |
| DELETE | `/atividades-os/:id` | Só concluída/cancelada; se for a última, exclui a OS; senão renumera ([[P6.7 - Excluir]]) |

## Orçamentos
| Método | Rota | Descrição |
| --- | --- | --- |
| GET | `/orcamentos` | Lista `id, cliente, criado_em, status, total`, do mais recente para o mais antigo ([[RF 4.14]]) |
| POST | `/orcamentos` | `{ cliente_id, endereco_id, observacao, itens[] }`; item: `{ tipo_atividade_id \| null, descricao, quantidade, valor_unitario, duracao_min }` ([[P4.1 - Montar orçamento]]) |
| GET | `/orcamentos/:id` | Orçamento com cliente, endereço, itens (com `tipo` ou `null` no avulso), `total` e `ordem_servico_id` |
| PUT | `/orcamentos/:id` | Só pendente; substitui dados e itens ([[P4.3 - Editar e excluir orçamento#RN 54\|RN 54]]) |
| DELETE | `/orcamentos/:id` | Só pendente; exclui os itens ([[P4.3 - Editar e excluir orçamento#RN 55\|RN 55]]) |
| POST | `/orcamentos/:id/aceitar` | `{ data, hora_inicio }` → `{ os_id, aviso_conflito }`; gera a OS encadeando um item por atividade; 409 se não couber no dia ([[P4.2 - Aceitar ou recusar orçamento]]) |
| POST | `/orcamentos/:id/recusar` | Só pendente ([[RF 4.12]]) |

O total é calculado em centavos a cada leitura, nunca gravado ([[P4.1 - Montar orçamento#RN 48|RN 48]]).

## Regra de conflito
Fica em um único lugar, `agenda.service.idsEmConflito`: há conflito entre atividades não canceladas, na mesma data, com intervalos sobrepostos. Atividades encostadas (o fim de uma igual ao início da outra) não conflitam.

Ver: [[Stack e Ambiente]], [[Frontend]]
