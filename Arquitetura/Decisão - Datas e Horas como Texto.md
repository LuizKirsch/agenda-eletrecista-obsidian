---
tags: [decisao]
status: aceita
data: 2026-09-27
---
# Decisão: Datas e Horas como Texto

## Contexto
A agenda trabalha com datas e horários locais (America/Sao_Paulo). Converter para `Date` do JavaScript causa deslocamentos de fuso entre servidor, banco e navegador, por exemplo uma atividade das 23h que aparece no dia seguinte.

## Decisão
Datas trafegam como `YYYY-MM-DD` e horários como `HH:MM`, sempre como texto. No banco, as colunas são `DATEONLY` e `TIME`. A aritmética (somar dias, dia da semana, minutos) é feita com inteiros pelo algoritmo *days_from_civil* de Howard Hinnant, em `services/horario.js` (backend) e `client/src/datas.js` (frontend), que têm a mesma implementação. Só "hoje" depende do relógio, calculado com `Intl.DateTimeFormat` no fuso America/Sao_Paulo.

## Justificativa
Sem conversão de fuso não há como a atividade mudar de dia. Comparar `HH:MM` como texto já dá a ordem correta, o que simplifica a regra de conflito ([[P1.5 - Verificar conflito de horário]]).

## Consequências
- Qualquer nova lógica de data deve usar `horario.js` ou `datas.js`, nunca `new Date(data)`.
- A atividade precisa começar e terminar no mesmo dia (fim ≤ 23:59) ([[P1.2 - Remarcar OS por arraste#RN 7|RN 7]]).
- As datas de registro (`criado_em`) continuam como DATETIME do banco e são formatadas com `Date` só para exibição.

Ver: [[Stack e Ambiente]]
