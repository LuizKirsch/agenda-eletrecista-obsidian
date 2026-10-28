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
| [[L1 - Anonimização no lugar do bloqueio de exclusão\|L1]] Anonimização no lugar do bloqueio de exclusão | RF V2.3, P3.4 (RN V2.3 a RN V2.5); muda [[RF 3.11]] e RN 42; `cliente.anonimizado_em` e `telefone` aceitando NULL |
| [[L2 - Exportação dos dados do cliente\|L2]] Exportação dos dados do cliente (JSON/CSV) | RF V2.4, P3.5 |
| [[L3 - Resumo Dados do titular\|L3]] Resumo "Dados do titular" em PDF | RF V2.5, P3.5 (RN V2.6 e RN V2.7) |
| [[L4 - Aviso no campo de observação\|L4]] Aviso no campo de observação | [[RF 3.13]] |
| [[L5 - Registro de acessos\|L5]] Registro de acessos (6 meses) | RF V2.1, RF V2.2, P2.5 (RN V2.1 e RN V2.2), entidade Registro de Acesso |
| [[L6 - Retenção dos dados\|L6]] Retenção dos dados (5 anos) | RF V2.6, P3.6 (RN V2.8 a RN V2.10) |
| [[L7 - Plano de resposta a incidentes\|L7]] Plano de resposta a incidentes | processo, a analisar |
| [[L8 - Política de privacidade e canal de contato\|L8]] Política de privacidade e canal de contato | processo, a analisar |
| [[L9 - Papéis e contrato controlador-operador\|L9]] Papéis e contrato controlador–operador | processo, a analisar |

- No MVP, o endereço continua obrigatório na OS ([[RF 6.1]]). Na V2, a anonimização (RF V2.3) apaga número, complemento e ponto de referência, mas o endereço continua existindo e vinculado à OS.
- Em 28/10/2026 os RFs e RNs da V2 saíram da doc; o texto proposto está nas notas L1, L2, L3, L5 e L6. O L4 ([[RF 3.13]]) ficou no MVP, porque já estava implementado.
- Os requisitos e as regras da V2 usam numeração provisória (RF V2.1 a RF V2.6, RN V2.1 a RN V2.10) e recebem número definitivo quando entrarem na doc. Em 28/10/2026 o antigo RF 3.16 (aviso no campo de observação) foi renumerado para RF 3.13, para a sequência do módulo não ter buraco.
