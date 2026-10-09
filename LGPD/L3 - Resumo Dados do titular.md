---
tags: [lgpd, ajuste]
id: "L3"
tipo: requisito
base: "LGPD art. 18, I e II; art. 19"
status: aceito
decisao: "RF 3.15"
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
Aceito como [[RF 3.15]], separado da exportação ([[RF 3.14]]): o resumo é o documento legível para enviar pelo WhatsApp; a exportação atende a portabilidade. Prazo e confirmação de identidade em [[P3.5 - Atender pedido do titular#RN 50|RN 50]].

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
