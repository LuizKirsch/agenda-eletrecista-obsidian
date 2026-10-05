---
tags: [requisito]
id: "RF 1.29"
modulo: "[[Agenda]]"
prioridade: Alta
alterado: false
entrega: 1
implementacao: parcial
---
# RF 1.29

na criação e na edição da OS, o sistema deve permitir buscar o cliente por parte do nome ou do telefone e, se ele não existir, cadastrá-lo (nome e telefone) sem sair do formulário; o mesmo vale para o endereço do cliente selecionado; ao escolher o endereço, suas observações são exibidas ([[RF 3.6]]).

**Módulo:** [[Agenda]]
**Entidades:** [[Ordem de Serviço]], [[Cliente]], [[Endereço]], [[Observação de Endereço]]

**Implementação:** o cliente é escolhido em um select com todos os clientes, sem busca, e não dá para cadastrar cliente nem endereço sem sair do formulário; as observações do endereço já são exibidas. Ver [[Status da Implementação]].

> Fonte: Documentação Técnica V6, seção 4.
