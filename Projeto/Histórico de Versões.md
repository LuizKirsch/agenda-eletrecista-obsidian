---
tags: [projeto]
---
# Histórico de Versões da Documentação

| Data | Versão | Autor |
| --- | --- | --- |
| 26/05/2022 | V1 | Edson I. Wobeto |
| 25/09/2026 | V2 | Luiz Kirsch |
| 25/09/2026 | V3 | Luiz Kirsch |
| 27/09/2026 | V4 | Luiz Kirsch |
| 27/09/2026 | V5 | Luiz Kirsch |
| 27/09/2026 | V6 | Luiz Kirsch |
| 05/10/2026 | V7 (em elaboração) | Luiz Kirsch |

## V2
Módulo [[Agenda]] revisado com base no protótipo navegável. O trabalho passa a ser organizado em Ordens de Serviço ([[Ordem de Serviço]]), cada uma composta por uma ou mais atividades com data, horário e status próprios.

## V3
O catálogo de tipos de atividade passa a ser gerenciável pelo usuário e é separado da Agenda em um módulo próprio, [[Atividade]].

## V4
Módulo [[Usuários e Acesso]] implementado: login, logout, manutenção da sessão e cadastro de usuários. A secretária é criada na instalação e cadastra o eletricista. Editar e excluir usuários passa a ser exclusivo da secretária.

## V5
Módulos [[Cliente e Endereço]], [[Atividade]] e [[Agenda]] implementados. Incluídos [[RF 3.8]] e [[RF 6.7|RF 1.28]]; alterados [[RF 1.5|RF 1.7]], [[RF 1.10|RF 1.14]], [[RF 1.8|RF 1.21]] e [[RF 1.11|RF 1.22]].

## V6
- Endereço obrigatório na OS ([[RF 6.1|RF 1.4]]); busca e cadastro de cliente/endereço sem sair do formulário ([[RF 6.2|RF 1.29]])
- Cliente, endereço e observação editáveis; exclusão só sem OS vinculada ([[RF 3.9]] a [[RF 3.12]])
- Telefone do cliente único e validado ([[RF 3.1]])
- Cadastro de usuários exclusivo da secretária ([[RF 2.9]])
- Atividades concluídas/canceladas travadas também na edição da OS ([[RF 6.11|RF 1.15]], [[RF 6.8|RF 1.17]])
- Histórico de OS por endereço/cliente e auditoria ficam [[Fora do MVP]]
- Regras do [[Orçamento (módulo)|Orçamento]] serão detalhadas na entrega 2

## V7 (em elaboração)
- Ordem de Serviço separada da [[Agenda]] em módulo próprio ([[Ordem de Serviço (módulo)|Ordem de Serviço]]): RF 6.1 a 6.19 e P6.1 a P6.8; Agenda renumerada para RF 1.1 a 1.12 e P1.1. RF 1.14 e RF 1.22 da V6 divididos entre os dois módulos. Ver [[Proposta - Módulo Ordem de Serviço]].
- Requisitos de LGPD ([[LGPD - Visão Geral]], L1 a L6): [[RF 2.14]], [[RF 2.15]] e [[RF 3.13]] a [[RF 3.17]]; processos [[P2.5 - Registrar acesso|P2.5]] e [[P3.4 - Anonimizar cliente|P3.4]] a [[P3.6 - Reter e eliminar dados|P3.6]] (RN 44 a RN 53); nova entidade [[Registro de Acesso]] e `cliente.anonimizado_em`. [[RF 3.11]] e RN 42 alterados para anonimizar, em vez de bloquear, cliente com OS vinculada.
