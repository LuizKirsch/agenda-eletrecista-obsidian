---
tags: [requisito]
id: "RF 6.23"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Média
alterado: true
entrega: 1
implementacao: completa
---
# RF 6.23

o sistema deve permitir exportar a Ordem de Serviço em PDF, em qualquer status, com cliente, telefone, endereço, eletricista responsável, observação da OS e a lista de atividades (tipo ou descrição, eletricista, data, início, fim e status), para levar ao atendimento ou entregar ao cliente (decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]], [[Cliente]], [[Endereço]], [[Usuário]]
**Implementação:** página `/os/:id/imprimir` (`OsImprimir.jsx`), aberta em nova aba pelo botão "Exportar PDF" do detalhe da OS, visível em qualquer status; o PDF sai pela impressão do navegador (`@media print`), como no [[RF 4.18]] (06/11/2026).
**Regras:** [[P6.4 - Editar OS inteira]] (a exportação vale também para a OS concluída ou cancelada, que é só leitura pela [[P6.4 - Editar OS inteira#RN 9|RN 9]])

> Origem: decisão do projeto (06/11/2026), no mesmo padrão do [[RF 4.18]] (exportar orçamento).
