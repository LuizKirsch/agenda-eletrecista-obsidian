---
tags: [decisao]
status: aceita
---
# Decisão: Arquitetura Monolítica

## Contexto
MVP com 5 módulos, 2 perfis de usuário e baixo acesso simultâneo.

## Decisão
Monólito: frontend React servido pelo próprio Express, uma única API e um banco MySQL em uma VPS.

## Justificativa
O escopo do MVP, a quantidade de perfis e o volume de acesso não justificam a complexidade de serviços separados. Em contexto acadêmico, a escolha fica documentada com a justificativa para mostrar que foi intencional.

Ver: [[Stack e Ambiente]]
