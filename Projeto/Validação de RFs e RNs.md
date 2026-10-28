---
tags: [projeto]
data: 2026-10-27
---
# Validação de RFs e RNs

Revisão de todas as RFs (88) e RNs (55 + 10 da V2) em 27/10/2026, cruzando umas com as outras e com o dicionário de dados. A numeração está íntegra. Foram achados 4 furos graves, 9 lacunas e 6 ajustes de redação; todos foram tratados nas próprias notas, e os que mudavam comportamento também no código.

## Graves

| # | Furo | Como ficou |
| --- | --- | --- |
| 1 | Cliente com orçamento aceito ou recusado nunca podia ser excluído: a [[P3.3 - Editar e excluir cliente, endereço e observação#RN 42\|RN 42]] bloqueava por orçamento e a [[P4.3 - Editar e excluir orçamento#RN 54\|RN 54]] só exclui orçamento pendente. Na V2, quem tinha só orçamento não podia ser excluído nem anonimizado | Só OS bloqueia; os orçamentos são excluídos junto ([[P3.3 - Editar e excluir cliente, endereço e observação#RN 42\|RN 42]], [[P3.3 - Editar e excluir cliente, endereço e observação#RN 43\|RN 43]], [[RF 3.11]]); código ajustado |
| 2 | A [[P5.1 - Gerenciar tipos de atividade#RN 21\|RN 21]] (sem tipo ativo não cria OS) contradizia a [[P4.2 - Aceitar ou recusar orçamento#RN 51\|RN 51]] (o aceite gera OS mesmo assim) | A RN 21 e o [[RF 5.8]] valem só para a criação manual |
| 3 | Editar a OS podia trocar o cliente de uma OS gerada por orçamento | [[P6.4 - Editar OS inteira#RN 57\|RN 57]]: o cliente fica travado; [[RF 6.8]] ajustado; API recusa (409) e o formulário desabilita o campo |
| 4 | Orçamento com mais de 24 h de serviço nunca podia ser aceito ([[P4.2 - Aceitar ou recusar orçamento#RN 52\|RN 52]]) | Revisto em 28/10/2026: o aceite gera OS em vários dias ([[P4.2 - Aceitar ou recusar orçamento#RN 51\|RN 51]], [[P4.2 - Aceitar ou recusar orçamento#RN 52\|RN 52]], [[RF 4.13]]); o item que não cabe vai para o dia seguinte e cada data é ajustável; sem limite na soma dos tempos ([[P4.1 - Montar orçamento#RN 47\|RN 47]]) |

## Lacunas

| # | Lacuna | Como ficou |
| --- | --- | --- |
| 5 | Excluir a OS gerada por orçamento não tinha regra | [[P4.2 - Aceitar ou recusar orçamento#RN 56\|RN 56]]: desfaz o vínculo, o orçamento continua aceito e não é aceito de novo; [[P6.7 - Excluir#RN 16\|RN 16]] aponta para ela |
| 6 | [[RF 4.7]] falava em vínculo manual que nenhuma regra descrevia | Reescrito: o vínculo nasce só do aceite |
| 7 | O tempo sugerido (quantidade × duração) podia passar de 720 min | [[P4.1 - Montar orçamento#RN 45\|RN 45]]: limitado a 720 |
| 8 | Fim calculado depois de 23h59 não tinha regra | [[P6.1 - Criar OS#RN 3\|RN 3]]: fim no mesmo dia; o usuário ajusta |
| 9 | Atividade avulsa na edição da OS | [[P6.4 - Editar OS inteira#RN 58\|RN 58]]: descrição fixa, só data e horários mudam |
| 10 | Concluir ou cancelar não tinha volta definida | [[P6.6 - Concluir ou cancelar#RN 59\|RN 59]]: não pode ser desfeito; corrige excluindo e cadastrando de novo |
| 11 | Editar cliente ou endereço muda o histórico | [[P3.3 - Editar e excluir cliente, endereço e observação#RN 61\|RN 61]]: OS e orçamento mostram os dados atuais (decisão registrada) |
| 12 | As regras de LGPD da V2 ignoravam o orçamento | [[P3.4 - Anonimizar cliente\|RN V2.3 e V2.4]], [[P3.5 - Atender pedido do titular\|RN V2.6]] e [[P3.6 - Reter e eliminar dados\|RN V2.8]] passam a incluir orçamentos |
| 13 | Datas no passado | [[P6.1 - Criar OS#RN 60\|RN 60]]: permitidas, para registrar serviço já feito |

## Redação

| # | Ajuste |
| --- | --- |
| 14 | [[P6.7 - Excluir#RN 14\|RN 14]] diz "pelo detalhe da OS", sem contradizer a [[P6.4 - Editar OS inteira#RN 9\|RN 9]] |
| 15 | [[P6.6 - Concluir ou cancelar#RN 12\|RN 12]] remete à RN 5 e cobre também remarcação e edição |
| 16 | [[P6.1 - Criar OS#RN 1\|RN 1]] inclui o endereço |
| 17 | [[P6.4 - Editar OS inteira#RN 35\|RN 35]] cobre também a exclusão pelo detalhe |
| 18 | [[RF 6.5]] e [[RF 6.7]] continuam sobrepostos; sem mudança |
| 19 | [[RF 1.5]] reescrito para o menu principal do layout novo |

## Status corrigido
- [[RF 1.5]]: completa, depois de reescrito.
- [[RF 3.16]]: já estava implementado (aviso no formulário de observação), apesar de listado na V2.

## Para o grupo decidir
- [[P6.6 - Concluir ou cancelar#RN 59|RN 59]] e [[P3.3 - Editar e excluir cliente, endereço e observação#RN 61|RN 61]] registram o comportamento atual; vale confirmar se é o desejado.

Ver também: [[Status da Implementação]]
