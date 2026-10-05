---
tags: [requisito]
id: "RF 3.1"
modulo: "[[Cliente e Endereço]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: parcial
---
# RF 3.1

O sistema deve permitir cadastrar cliente com campos mínimos: nome e telefone; o telefone deve ter DDD e 8 ou 9 dígitos, é exibido com máscara e não pode se repetir entre clientes (alterado: decisão do projeto);

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Cliente]]

**Implementação:** nome e telefone já são obrigatórios, mas o telefone não tem validação de DDD + 8/9 dígitos, não tem máscara e `cliente.telefone` não é UNIQUE. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
