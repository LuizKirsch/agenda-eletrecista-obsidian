---
tags: [requisito]
id: "RF 6.21"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 6.21

toda OS deve ter um eletricista responsável, escolhido na criação e na edição da OS (decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Ordem de Serviço]], [[Usuário]]
**Implementação:** `ordem_servico.eletricista_id`; a API exige o responsável e recusa usuário inativo ou de outro perfil (06/11/2026). A coluna aceita NULL no banco, ver [[Ordem de Serviço]].
**Regras:** [[P6.1 - Criar OS]]

> Origem: pedido do professor na apresentação de 28/10/2026.
