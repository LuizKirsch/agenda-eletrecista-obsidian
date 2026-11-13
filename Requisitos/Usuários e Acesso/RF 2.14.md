---
tags: [requisito]
id: "RF 2.14"
modulo: "[[Usuários e Acesso]]"
prioridade: Média
alterado: true
entrega: 3
implementacao: completa
---
# RF 2.14

o eletricista com atividades vinculadas não pode ser excluído, apenas desativado; o eletricista inativo deixa de ser oferecido para novas OS e atividades, mas permanece nas já registradas (decisão do projeto);

**Módulo:** [[Usuários e Acesso]]
**Entidades:** [[Usuário]], [[Atividade da OS]]
**Implementação:** `DELETE /api/usuarios/:id` devolve 409 se o eletricista tem OS ou atividades; a FK `eletricista_id` é RESTRICT; inativo não é oferecido em seleções novas (06/11/2026). Trocar o perfil de um eletricista com vínculos não é bloqueado.
**Regras:** [[P2.3 - Cadastrar, editar e excluir usuário]]

> Origem: pedido do professor na apresentação de 28/10/2026.
