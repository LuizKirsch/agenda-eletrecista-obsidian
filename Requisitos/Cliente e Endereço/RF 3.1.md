---
tags: [requisito]
id: "RF 3.1"
modulo: "[[Cliente e Endereço]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 3.1

O sistema deve permitir cadastrar cliente com campos mínimos: nome e telefone; o telefone deve ter DDD e 8 ou 9 dígitos, é exibido com máscara e não pode se repetir entre clientes (alterado: decisão do projeto);

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Cliente]]

**Implementação:** validação de DDD + 8/9 dígitos, máscara na tela e unicidade em `cliente.service.validarTelefone`; o banco guarda só os dígitos (06/11/2026). A coluna ainda não é UNIQUE, ver [[Cliente]].

> Fonte: Documentação Técnica V6, seção 4.
