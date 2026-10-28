---
tags: [lgpd, ajuste]
id: "L3"
tipo: requisito
base: "LGPD art. 18, I e II; art. 19"
status: aceito
decisao: "RF V2.5"
versao: V2
---
# L3 – Resumo "Dados do titular" na ficha do cliente

**Base:** LGPD art. 18, I e II; art. 19 · **Tipo:** requisito novo

## O que a apresentação propõe
Gerar na ficha do cliente um resumo "Dados do titular" (ex.: PDF de uma página) que a secretária envia quando o cliente pedir pelo WhatsApp. Confirmação imediata; resposta completa em até 15 dias.

## Por que não estava no projeto
O cliente não tem login, então o atendimento dos direitos fica do lado de quem usa o sistema (secretária), e isso não estava previsto.

## Onde impacta
- [[Cliente e Endereço]] — nova ação na ficha do cliente
- [[Usuários e Acesso]] — quem pode gerar o resumo
- Processo: confirmar identidade pelo telefone cadastrado antes de enviar

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Avaliar se pode ser a mesma funcionalidade da [[L2 - Exportação dos dados do cliente|L2]]
- [x] Definir número de RF (módulo 3)

## Decisão
Aceito como RF V2.5, separado da exportação (RF V2.4): o resumo é o documento legível para enviar pelo WhatsApp; a exportação atende a portabilidade. Prazo e confirmação de identidade em RN V2.7.

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].

## Texto proposto para a V2

> Retirado da doc em 28/10/2026, junto com os demais RFs e RNs de LGPD; guardado aqui para quando a V2 começar. A numeração é provisória.

**RF V2.5** — o sistema deve gerar, na ficha do cliente, um resumo "Dados do titular" em PDF de uma página, com o cadastro, os endereços, as observações e a relação das OS do cliente, para envio ao titular quando ele solicitar;

**P3.5 - Atender pedido do titular**

#### RN V2.6
A exportação e o resumo "Dados do titular" incluem o cadastro do cliente, seus endereços, as observações dos endereços, as OS com suas atividades e os orçamentos com seus itens;

#### RN V2.7
Antes de enviar os dados, a secretária confirma a identidade do titular pelo telefone cadastrado; o pedido é confirmado na hora e a resposta completa é enviada em até 15 dias.
