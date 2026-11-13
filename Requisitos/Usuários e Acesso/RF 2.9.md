---
tags: [requisito]
id: "RF 2.9"
modulo: "[[Usuários e Acesso]]"
prioridade: Alta
alterado: true
entrega: 3
implementacao: completa
---
# RF 2.9

somente a secretária pode cadastrar usuário, informando nome, login, senha e perfil (alterado: decisão do projeto);

**Módulo:** [[Usuários e Acesso]]
**Entidades:** [[Usuário]]

**Implementação:** `POST /api/usuarios` usa `somenteSecretaria` (403 para o eletricista) (06/11/2026).

> Fonte: Documentação Técnica V6, seção 4.
