---
tags: [projeto]
---
# Fora do MVP

- Acesso do cliente final / auto agendamento
- Check-in e checkout com foto (backlog 14 e 15) — não validado como dor prioritária; risco de dependência de conexão em campo
- Modo offline robusto
- Consulta do histórico de OS por endereço ou por cliente
- Registro de quem criou ou alterou cada registro

## V2 do app

### LGPD (adiado em 19/10/2026)
Ajustes levantados em [[LGPD - Visão Geral]]. Ficam fora do MVP e da doc V7.

| Ajuste | Requisitos e regras |
| --- | --- |
| [[L1 - Anonimização no lugar do bloqueio de exclusão\|L1]] Anonimização no lugar do bloqueio de exclusão | [[RF 3.13]], [[P3.4 - Anonimizar cliente\|P3.4]] (RN V2.3 a RN V2.5); muda [[RF 3.11]] e RN 42; `cliente.anonimizado_em` e `telefone` aceitando NULL |
| [[L2 - Exportação dos dados do cliente\|L2]] Exportação dos dados do cliente (JSON/CSV) | [[RF 3.14]], [[P3.5 - Atender pedido do titular\|P3.5]] |
| [[L3 - Resumo Dados do titular\|L3]] Resumo "Dados do titular" em PDF | [[RF 3.15]], [[P3.5 - Atender pedido do titular\|P3.5]] (RN V2.6 e RN V2.7) |
| [[L4 - Aviso no campo de observação\|L4]] Aviso no campo de observação | [[RF 3.16]] |
| [[L5 - Registro de acessos\|L5]] Registro de acessos (6 meses) | [[RF 2.14]], [[RF 2.15]], [[P2.5 - Registrar acesso\|P2.5]] (RN V2.1 e RN V2.2), entidade [[Registro de Acesso]] |
| [[L6 - Retenção dos dados\|L6]] Retenção dos dados (5 anos) | [[RF 3.17]], [[P3.6 - Reter e eliminar dados\|P3.6]] (RN V2.8 a RN V2.10) |
| [[L7 - Plano de resposta a incidentes\|L7]] Plano de resposta a incidentes | processo, a analisar |
| [[L8 - Política de privacidade e canal de contato\|L8]] Política de privacidade e canal de contato | processo, a analisar |
| [[L9 - Papéis e contrato controlador-operador\|L9]] Papéis e contrato controlador–operador | processo, a analisar |

- No MVP, o endereço continua obrigatório na OS ([[RF 6.1]]). Na V2, a anonimização ([[RF 3.13]]) apaga número, complemento e ponto de referência, mas o endereço continua existindo e vinculado à OS.
- Os números RF 2.14, RF 2.15 e RF 3.13 a RF 3.17 ficam reservados para a V2. As regras de negócio da V2 usam numeração provisória (RN V2.1 a RN V2.10) e recebem o número definitivo quando entrarem na doc; a sequência RN 44 em diante segue no MVP.
