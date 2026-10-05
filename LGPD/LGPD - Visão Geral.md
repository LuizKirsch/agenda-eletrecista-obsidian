---
tags: [lgpd, indice]
---
# LGPD – Visão Geral

Pontos levantados na apresentação **"A LGPD dentro de uma agenda de eletricista"** (05/10/2026) que **não estavam no projeto original** (Documentação Técnica V6). Ficam aqui para análise; o que for aceito vira RF/RN e é levado para a documentação técnica.

Apresentação: https://claude.ai/artifact/AvtLwR4fPsRSEkyPZgnAst

## Já previsto no projeto
- Correção dos dados (art. 18, III) — edição de cliente, endereço e observação ([[P3.3 - Editar e excluir cliente, endereço e observação]])
- Cadastro mínimo, sem CPF/documento/dado bancário (art. 6º, III) — [[RF 3.1]]
- Segurança (art. 46) — [[Requisitos Não Funcionais|RNF-6]]: bcrypt, JWT em cookie httpOnly, rotas autenticadas; usuário inativo perde a sessão ([[RF 2.5]])

## Ajustes pendentes
| ID | Ajuste | Tipo | Base | Status |
| --- | --- | --- | --- | --- |
| [[L1 - Anonimização no lugar do bloqueio de exclusão\|L1]] | Anonimização no lugar do bloqueio de exclusão | requisito | LGPD art. 18, IV | a analisar |
| [[L2 - Exportação dos dados do cliente\|L2]] | Exportação dos dados do cliente | requisito | LGPD art. 18, V | a analisar |
| [[L3 - Resumo Dados do titular\|L3]] | Resumo "Dados do titular" na ficha do cliente | requisito | LGPD art. 18, I e II; art. 19 | a analisar |
| [[L4 - Aviso no campo de observação\|L4]] | Aviso no campo de observação | requisito | LGPD art. 6º, III; art. 11; art. 14 | a analisar |
| [[L5 - Registro de acessos\|L5]] | Registro de acessos (6 meses) | requisito | Marco Civil art. 15; LGPD art. 7º, II | a analisar |
| [[L6 - Retenção dos dados\|L6]] | Política de retenção | regra | LGPD art. 15 e 16; CDC art. 27 | a analisar |
| [[L7 - Plano de resposta a incidentes\|L7]] | Plano de resposta a incidentes | processo | LGPD art. 46 e 48; Resolução CD/ANPD nº 15/2024 | a analisar |
| [[L8 - Política de privacidade e canal de contato\|L8]] | Política de privacidade e canal de contato | processo | LGPD art. 9º e 41; Resolução CD/ANPD nº 2/2022 | a analisar |
| [[L9 - Papéis e contrato controlador-operador\|L9]] | Papéis e contrato controlador–operador | processo | LGPD art. 5º, VI e VII; art. 39 | a analisar |

**Tipos:** `requisito` = muda o sistema · `regra` = regra de negócio · `processo` = documento ou procedimento fora do código.

## Como trabalhar
1. Analisar cada nota e marcar o checklist.
2. Preencher **Decisão** e mudar o `status` no frontmatter (`a analisar` → `aceito` / `fora do MVP` / `descartado`).
3. Aceito como requisito: criar o RF pelo template [[Requisito]] no módulo certo e linkar aqui.
4. Fora do MVP: registrar em [[Fora do MVP]].

Template para novos pontos: [[Ajuste LGPD]].
