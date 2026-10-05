---
tags: [indice]
---
# Agenda do Eletricista — Visão Geral

Sistema de agenda e gestão de Ordens de Serviço para um eletricista autônomo e sua secretária. Projeto acadêmico (ADS/IENH), baseado na Documentação Técnica V6.

## Projeto
- [[Contexto e Cliente]]
- [[Planejamento de Entregas]]
- [[Backlog]]
- [[Histórico de Versões]]
- [[Status da Implementação]]
- [[Histórico de Commits]]
- [[Fora do MVP]]

## Módulos
- [[Agenda]] — entrega 1
- [[Usuários e Acesso]] — entrega 3
- [[Cliente e Endereço]] — entrega 1
- [[Orçamento (módulo)|Orçamento]] — entrega 2
- [[Atividade]] — entrega 1

## Domínio
- [[Usuário]]
- [[Cliente]]
- [[Endereço]]
- [[Observação de Endereço]]
- [[Tipo de Atividade]]
- [[Ordem de Serviço]]
- [[Atividade da OS]]
- [[Orçamento]]
- [[Item de Serviço]]

Mapa visual: [[Mapa do Domínio.canvas|Mapa do Domínio]]

## Requisitos
- Tabela filtrável: [[Requisitos.base|Requisitos]] (por módulo, prioridade, alterado, implementação)
- [[Requisitos Não Funcionais]]

## Regras de negócio
- [[P1.1 - Criar OS]]
- [[P1.2 - Remarcar OS por arraste]]
- [[P1.3 - Remarcar atividade]]
- [[P1.4 - Editar OS inteira]]
- [[P1.5 - Verificar conflito de horário]]
- [[P1.6 - Concluir ou cancelar]]
- [[P1.7 - Excluir]]
- [[P1.8 - Adicionar atividade a OS existente]]
- [[P5.1 - Gerenciar tipos de atividade]]
- [[P2.1 - Autenticar]]
- [[P2.2 - Cadastrar usuário]]
- [[P2.3 - Cadastrar, editar e excluir usuário]]
- [[P2.4 - Criar usuário inicial]]
- [[P3.1 - Cadastrar cliente, endereço e observação]]
- [[P3.2 - Buscar cliente]]
- [[P3.3 - Editar e excluir cliente, endereço e observação]]

## Arquitetura
- [[Stack e Ambiente]]
- [[API REST]]
- [[Frontend]]
- [[Decisão - Arquitetura Monolítica]]
- [[Decisão - Endereço como Entidade Própria]]
- [[Decisão - Datas e Horas como Texto]]
- [[Decisão - SQLite em Desenvolvimento]]
