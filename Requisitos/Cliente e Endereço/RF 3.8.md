---
tags: [requisito]
id: "RF 3.8"
modulo: "[[Cliente e Endereço]]"
prioridade: Alta
alterado: false
entrega: 1
implementacao: completa
---
# RF 3.8

o sistema deve listar os clientes em ordem alfabética, com busca por parte do nome ou do telefone, sem diferenciar maiúsculas, minúsculas e acentos; a listagem é a tela de entrada do módulo e oferece o botão "Novo cliente";

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Cliente]]

**Implementação:** a busca usa `LIKE`; no MySQL, maiúsculas e acentos são ignorados pela collation padrão (`utf8mb4_0900_ai_ci`), mas no SQLite de desenvolvimento os acentos são diferenciados. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
