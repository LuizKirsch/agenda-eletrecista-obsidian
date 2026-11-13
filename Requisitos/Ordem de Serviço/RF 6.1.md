---
tags: [requisito]
id: "RF 6.1"
id_v6: "RF 1.4"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 6.1

o sistema deve permitir criar uma Ordem de Serviço (OS) informando cliente, endereço, observações e uma ou mais atividades; cliente e endereço são obrigatórios, e o endereço deve pertencer ao cliente da OS (alterado: decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Ordem de Serviço]], [[Atividade da OS]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** a API exige o endereço e confere que é do cliente (400) (06/11/2026). A coluna `ordem_servico.endereco_id` continua aceitando NULL, ver [[Ordem de Serviço]].

> Fonte: Documentação Técnica V6, seção 4.
> Numeração V7 (separação do módulo Ordem de Serviço); na V6: RF 1.4.
