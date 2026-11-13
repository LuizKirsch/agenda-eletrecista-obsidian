---
tags: [requisito]
id: "RF 2.11"
modulo: "[[Usuários e Acesso]]"
prioridade: Média
alterado: true
entrega: 3
implementacao: completa
---
# RF 2.11

somente a secretária pode excluir usuário, com confirmação na tela; a exclusão remove o registro definitivamente, exceto o eletricista com atividades vinculadas ([[RF 2.14]]) (alterado: decisão do projeto);

**Módulo:** [[Usuários e Acesso]]
**Entidades:** [[Usuário]]
**Implementação:** exclusão só pela secretária, com confirmação em modal; eletricista com vínculos devolve 409 ([[RF 2.14]]) (06/11/2026).

> Fonte: Documentação Técnica V6, seção 4.
> Alterado pelo pedido do professor (28/10/2026).
