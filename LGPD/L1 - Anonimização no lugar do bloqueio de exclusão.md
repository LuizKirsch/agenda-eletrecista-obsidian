---
tags: [lgpd, ajuste]
id: "L1"
tipo: requisito
base: "LGPD art. 18, IV"
status: aceito
decisao: "RF 3.13"
---
# L1 – Anonimização no lugar do bloqueio de exclusão

**Base:** LGPD art. 18, IV · **Tipo:** requisito do sistema (altera regra existente)

## O que a apresentação propõe
Quando o cliente pedir a eliminação e houver OS vinculada, anonimizar em vez de bloquear:
- nome vira "Cliente anonimizado nº X";
- telefone apagado;
- número, complemento e referência do endereço apagados;
- observações excluídas;
- as OS permanecem, sem identificar a pessoa.

## Por que não estava no projeto
A regra atual impede excluir cliente com OS vinculada, o que na prática bloqueia o direito de eliminação do titular.

## Onde impacta
- [[RF 3.11]] — conflito direto com a regra de exclusão
- [[P3.3 - Editar e excluir cliente, endereço e observação#RN 42|RN 42]] e [[P3.3 - Editar e excluir cliente, endereço e observação#RN 43|RN 43]]
- [[Cliente]] — `telefone` hoje é NOT NULL + UNIQUE; precisaria ser opcional; nova coluna de data da anonimização
- [[Endereço]] e [[Observação de Endereço]]
- [[Ordem de Serviço]] — continua referenciando o cliente anonimizado

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir se é ação manual da secretária ou automática
- [ ] Revisar unicidade do telefone com telefone nulo
- [x] Atualizar RF 3.11 / RN 42 na documentação técnica

## Decisão
Aceito como [[RF 3.13]] e [[P3.4 - Anonimizar cliente]] (RN 46 a RN 48). Ação manual na ficha do cliente, com confirmação e irreversível. A exclusão do [[RF 3.11]] continua valendo para cliente sem OS; com OS vinculada, a alternativa passa a ser a anonimização. Em [[Cliente]], `telefone` deixa de ser NOT NULL (UNIQUE aceita vários NULL no MySQL) e entra `anonimizado_em`.

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
