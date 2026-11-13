---
tags: [requisito]
id: "RF 6.22"
modulo: "[[Ordem de Serviço (módulo)]]"
prioridade: Alta
alterado: true
entrega: 1
implementacao: completa
---
# RF 6.22

cada atividade da OS deve ter um eletricista, sugerido como o responsável pela OS e alterável por atividade, de modo que uma mesma OS pode ter eletricistas diferentes em atividades diferentes (decisão do projeto);

**Módulo:** [[Ordem de Serviço (módulo)|Ordem de Serviço]]
**Entidades:** [[Atividade da OS]], [[Usuário]]
**Implementação:** `atividade_os.eletricista_id`; a atividade herda o responsável da OS e pode ser trocada no formulário (06/11/2026). Remarcar ou arrastar não troca o eletricista.
**Regras:** [[P6.1 - Criar OS]]

> Origem: pedido do professor na apresentação de 28/10/2026.
