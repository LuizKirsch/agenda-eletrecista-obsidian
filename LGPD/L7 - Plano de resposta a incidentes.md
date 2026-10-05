---
tags: [lgpd, ajuste]
id: "L7"
tipo: processo
base: "LGPD art. 46 e 48; Resolução CD/ANPD nº 15/2024"
status: a analisar
decisao:
---
# L7 – Plano de resposta a incidentes

**Base:** LGPD art. 46 e 48; Resolução CD/ANPD nº 15/2024 · **Tipo:** processo / documento

## O que a apresentação propõe
1. Conter: trocar o segredo do JWT derruba todas as sessões.
2. Avisar o eletricista em até 24 horas.
3. Comunicar ANPD e titulares em 3 dias úteis, se houver risco relevante (prazo em dobro para agente de pequeno porte).
4. Registrar o incidente e guardar por 5 anos.

## Por que não estava no projeto
As medidas de segurança já existiam ([[Requisitos Não Funcionais|RNF-6]]), mas não havia plano para vazamento.

## Onde impacta
- [[Requisitos Não Funcionais]]
- [[Stack e Ambiente]] — como trocar o `JWT_SECRET` em produção
- Documento à parte (não é funcionalidade do sistema)

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Decidir se vira seção da documentação técnica ou anexo

## Decisão
_A preencher após a análise._

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
