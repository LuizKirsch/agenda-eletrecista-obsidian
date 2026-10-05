---
tags: [requisito]
id: "RF 1.4"
modulo: "[[Agenda]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: parcial
---
# RF 1.4

o sistema deve permitir criar uma Ordem de Serviço (OS) informando cliente, endereço, observações e uma ou mais atividades; cliente e endereço são obrigatórios, e o endereço deve pertencer ao cliente da OS (alterado: decisão do projeto);

**Módulo:** [[Agenda]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** o endereço ainda é opcional: o formulário oferece "Sem endereço", a API só valida o endereço quando ele é enviado e `ordem_servico.endereco_id` aceita NULL. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
