---
tags: [modulo]
entrega: 3
---
# Usuários e Acesso

Define os perfis de acesso ao sistema: eletricista e secretária. Os dois perfis têm acesso às mesmas funcionalidades, com uma exceção: cadastrar, editar e excluir usuários é exclusivo da secretária. O módulo cobre login, logout, manutenção da sessão e cadastro de usuários. Não há registro de qual usuário criou ou alterou cada informação nesta versão. O usuário inicial da secretária é criado na instalação do sistema, e ela cadastra o eletricista pelo próprio sistema. Não há acesso do cliente final ao sistema nesta versão.

## Entidades
- [[Usuário]]

## Processos e regras de negócio
- [[P2.1 - Autenticar]]
- [[P2.2 - Cadastrar usuário]]
- [[P2.3 - Cadastrar, editar e excluir usuário]]
- [[P2.4 - Criar usuário inicial]]

## Requisitos funcionais (13)
- [[RF 2.1]] (Alta) — O sistema deve reconhecer o login de dois tipos de usuário: eletricista e secretária
- [[RF 2.2]] (Alta) — ambos os perfis devem ter acesso às mesmas funcionalidades (agenda, atividade, cliente, orçamento e listagem d…
- [[RF 2.3]] (Média) — não deve existir tela ou dado exclusivo de um perfil sobre o outro, com exceção das ações de cadastrar, editar…
- [[RF 2.4]] (Alta) — o sistema deve autenticar o usuário por login e senha; em caso de falha, deve exibir mensagem genérica, sem in…
- [[RF 2.5]] (Alta) — usuário inativo não deve conseguir entrar no sistema, e as sessões já abertas por ele devem ser encerradas na…
- [[RF 2.6]] (Alta) — o sistema deve permitir que o usuário saia do sistema (logout)
- [[RF 2.7]] (Alta) — a sessão deve permanecer ativa ao recarregar a página ou reabrir o navegador, enquanto for válida (padrão: 7 d…
- [[RF 2.8]] (Alta) — o sistema deve listar os usuários com nome, login, perfil e situação (ativo/inativo), para ambos os perfis
- [[RF 2.9]] (Alta) — somente a secretária pode cadastrar usuário, informando nome, login, senha e perfil (alterado: decisão do proj…
- [[RF 2.10]] (Média) — somente a secretária pode editar usuário (nome, login, perfil, situação e senha); a senha em branco mantém a s…
- [[RF 2.11]] (Média) — somente a secretária pode excluir usuário, com confirmação na tela; a exclusão remove o registro definitivamen…
- [[RF 2.12]] (Média) — a secretária não pode excluir, desativar nem alterar o perfil do próprio usuário
- [[RF 2.13]] (Alta) — o usuário inicial com perfil secretária deve ser criado pela migration da tabela usuario, com nome, login e se…

Voltar: [[00 - Visão Geral]]
