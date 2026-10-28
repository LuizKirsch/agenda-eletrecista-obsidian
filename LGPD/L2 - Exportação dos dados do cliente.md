---
tags: [lgpd, ajuste]
id: "L2"
tipo: requisito
base: "LGPD art. 18, V"
status: aceito
decisao: "RF V2.4"
versao: V2
---
# L2 – Exportação dos dados do cliente

**Base:** LGPD art. 18, V · **Tipo:** requisito novo

## O que a apresentação propõe
Exportar os dados de um cliente (cadastro, endereços, observações e OS) em JSON e CSV.

## Por que não estava no projeto
O projeto não previa nenhuma exportação; a portabilidade é direito do titular.

## Onde impacta
- [[Cliente e Endereço]] — nova ação na ficha do cliente
- [[API REST]] — nova rota de exportação
- [[Backlog]] — novo item

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir formato(s) realmente necessários (JSON, CSV ou ambos)
- [x] Definir número de RF (módulo 3)

## Decisão
Aceito como RF V2.4, com os dois formatos propostos (JSON e CSV). Regras em P3.5 - Atender pedido do titular (RN V2.6 e RN V2.7).

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].

## Texto proposto para a V2

> Retirado da doc em 28/10/2026, junto com os demais RFs e RNs de LGPD; guardado aqui para quando a V2 começar. A numeração é provisória.

**RF V2.4** — o sistema deve permitir exportar, a partir da ficha do cliente, os dados do cliente (cadastro, endereços, observações e OS com suas atividades) em JSON e em CSV;

**P3.5 - Atender pedido do titular**

#### RN V2.6
A exportação e o resumo "Dados do titular" incluem o cadastro do cliente, seus endereços, as observações dos endereços, as OS com suas atividades e os orçamentos com seus itens;

#### RN V2.7
Antes de enviar os dados, a secretária confirma a identidade do titular pelo telefone cadastrado; o pedido é confirmado na hora e a resposta completa é enviada em até 15 dias.
