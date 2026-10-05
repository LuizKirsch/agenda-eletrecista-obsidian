---
tags: [requisito]
id: "RF 2.9"
modulo: "[[Usuários e Acesso]]"
prioridade: Alta
alterado: true
entrega: 3
implementacao: parcial
---
# RF 2.9

somente a secretária pode cadastrar usuário, informando nome, login, senha e perfil (alterado: decisão do projeto);

**Módulo:** [[Usuários e Acesso]]
**Entidades:** [[Usuário]]

**Implementação:** `POST /api/usuarios` não usa o middleware `somenteSecretaria`, e a tela de Usuários mostra o formulário de cadastro para os dois perfis. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
