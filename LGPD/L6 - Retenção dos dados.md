---
tags: [lgpd, ajuste]
id: "L6"
tipo: regra
base: "LGPD art. 15 e 16; CDC art. 27"
status: aceito
decisao: "RF V2.6"
versao: V2
---
# L6 – Política de retenção

**Base:** LGPD art. 15 e 16; CDC art. 27 · **Tipo:** regra de negócio / processo

## O que a apresentação propõe
Guardar cliente, endereço, observações e OS por 5 anos após o último serviço (prazo do art. 27 do CDC); usuários enquanto ativos; registros de acesso por 6 meses.

## Por que não estava no projeto
O projeto não define quando os dados deixam de ser necessários. O [[Requisitos Não Funcionais|RNF-5]] só fala em persistência e backup.

## Onde impacta
- [[Requisitos Não Funcionais]] — RNF-5
- [[Cliente]] / [[Ordem de Serviço]] — data do último serviço
- Liga com a [[L1 - Anonimização no lugar do bloqueio de exclusão|L1]] (o que fazer ao fim do prazo)

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Decidir se o expurgo/anonimização ao fim do prazo é automático ou manual

## Decisão
Aceito como RF V2.6 e P3.6 - Reter e eliminar dados (RN V2.8 a RN V2.10). O último serviço é a data da última atividade concluída do cliente. Ao fim dos 5 anos o sistema só sinaliza; anonimizar ou excluir continua sendo ação manual.

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].

## Texto proposto para a V2

> Retirado da doc em 28/10/2026, junto com os demais RFs e RNs de LGPD; guardado aqui para quando a V2 começar. A numeração é provisória.

**RF V2.6** — o sistema deve sinalizar na listagem de clientes aqueles cujo último serviço tenha mais de 5 anos, para que sejam anonimizados (RF V2.3) ou excluídos ([[RF 3.11]]);

**P3.6 - Reter e eliminar dados**

#### RN V2.8
Cliente, endereços, observações e OS são guardados por 5 anos após o último serviço, contado pela data da última atividade concluída do cliente; sem atividade concluída, conta pela data do último orçamento ou, na falta dele, pela data de cadastro;

#### RN V2.9
Usuários são mantidos enquanto ativos, e os registros de acesso, por 6 meses (RN V2.2);

#### RN V2.10
Ao fim do prazo, o sistema sinaliza o cliente e o usuário decide entre anonimizá-lo (P3.4) ou excluí-lo ([[P3.3 - Editar e excluir cliente, endereço e observação|P3.3]]).
