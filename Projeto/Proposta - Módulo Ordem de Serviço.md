---
tags: [projeto, proposta]
status: aplicada
data: 2026-10-05
versao_alvo: V7
---
# Proposta – Separar o módulo Ordem de Serviço

Hoje a OS vive dentro do módulo [[Agenda]] (RF 1.1 a 1.29, processos P1.1 a P1.8). A proposta é dividir em dois módulos e levar a mudança para a doc **V7**, junto com os ajustes de [[LGPD - Visão Geral|LGPD]] e a troca de nome do projeto.

> **Aplicada em 05/10/2026.** Na coluna "Atual", os links abrem o arquivo já renumerado e mostram o número da V6.

## Critério de fronteira
- **Agenda**: *como se vê e se move*. A visão semanal, a navegação, os blocos na tela e os gestos (clicar e arrastar).
- **Ordem de Serviço**: *o que a OS é e quais regras ela segue*. Criar, editar, gerenciar atividades, mudar status, excluir e verificar conflito.
- Quando a ação acontece na tela mas muda dados (arrastar, abrir um bloco), **o gesto fica na Agenda e a regra fica na OS**. A Agenda chama a OS.

Numeração: OS = **RF 6.x / P6.x** (o 5 já é [[Atividade]]). Os números de RN são globais e **não mudam**.

## Requisitos – Agenda (fica com 12)
| Novo | Atual | Resumo | Obs. |
| --- | --- | --- | --- |
| RF 1.1 | [[RF 1.1|RF 1.1]] | Visão semanal, seg–dom, 00h–23h59 | |
| RF 1.2 | [[RF 1.2|RF 1.2]] | Navegar entre semanas | |
| RF 1.3 | [[RF 1.3|RF 1.3]] | Destacar dia atual | |
| RF 1.4 | [[RF 1.4|RF 1.5]] | Clicar em horário livre abre a criação da OS | chama RF 6.1 |
| RF 1.5 | [[RF 1.5|RF 1.7]] | Botão para tipos de atividade | |
| RF 1.6 | [[RF 1.6|RF 1.11]] | Distinção visual por status | o status em si está em RF 6.3 |
| RF 1.7 | [[RF 1.7|RF 1.12]] | Posição na OS no bloco (1/2 · OS 2) | |
| RF 1.8 | [[RF 1.8|RF 1.21]] | Blocos lado a lado e agrupados | |
| RF 1.9 | [[RF 1.9|RF 1.13]] | Arrastar com encaixe de 15 min | |
| RF 1.10 | [[RF 1.10|RF 1.14]] | **Dividido:** arrastar abre a pergunta (OS inteira / só a atividade / cancelar) | encadeamento vai para RF 6.10 |
| RF 1.11 | [[RF 1.11|RF 1.22]] | **Dividido:** selecionar um bloco abre a OS com a atividade selecionada | conteúdo do detalhe vai para RF 6.19 |
| RF 1.12 | [[RF 1.12|RF 1.27]] | Alterações refletem na hora | |

## Requisitos – Ordem de Serviço (19, sendo 2 vindos de divisão)
| Novo | Atual | Resumo |
| --- | --- | --- |
| RF 6.1 | [[RF 6.1|RF 1.4]] | Criar OS (cliente, endereço, observações, atividades) |
| RF 6.2 | [[RF 6.2|RF 1.29]] | Buscar ou cadastrar cliente e endereço sem sair da OS |
| RF 6.3 | [[RF 6.3|RF 1.6]] | Atividade com tipo, data, horários e status |
| RF 6.4 | [[RF 6.4|RF 1.8]] | Fim calculado pela duração padrão |
| RF 6.5 | [[RF 6.5|RF 1.9]] | Nova atividade sugere início no fim da anterior |
| RF 6.6 | [[RF 6.6|RF 1.10]] | Fim deve ser posterior ao início |
| RF 6.7 | [[RF 6.7|RF 1.28]] | Adicionar atividade a OS existente |
| RF 6.8 | [[RF 6.8|RF 1.17]] | Editar OS inteira |
| RF 6.9 | [[RF 6.9|RF 1.16]] | Remarcar uma atividade |
| RF 6.10 | [[RF 1.10|RF 1.14]] (parte) | **Novo:** regra de remarcar a OS inteira (encadeamento, mesmo dia, sem intervalos; se não couber, nada muda) |
| RF 6.11 | [[RF 6.11|RF 1.15]] | Concluídas/canceladas travadas |
| RF 6.12 | [[RF 6.12|RF 1.18]] | Sinalizar conflito (aparece na agenda e no detalhe) |
| RF 6.13 | [[RF 6.13|RF 1.19]] | Conflito não impede o salvamento |
| RF 6.14 | [[RF 6.14|RF 1.20]] | Canceladas fora do conflito |
| RF 6.15 | [[RF 6.15|RF 1.23]] | Concluir/cancelar atividade |
| RF 6.16 | [[RF 6.16|RF 1.24]] | Concluir OS inteira |
| RF 6.17 | [[RF 6.17|RF 1.25]] | Excluir atividade concluída/cancelada |
| RF 6.18 | [[RF 6.18|RF 1.26]] | Excluir OS inteira |
| RF 6.19 | [[RF 1.11|RF 1.22]] (parte) | **Novo:** conteúdo do detalhe da OS (cliente, telefone, endereço, observações, atividades, ações) |

Conferência: 12 + 17 = 29 RF atuais; RF 1.14 e RF 1.22 geram uma parte em cada módulo.

## Processos e regras de negócio
| Atual | Destino | Observação |
| --- | --- | --- |
| [[P6.1 - Criar OS|P1.1 - Criar OS]] (RN 1–4, 34, 40) | P6.1 – Criar OS | |
| [[P1.1 - Arrastar atividade|P1.2 - Remarcar OS por arraste]] | **Dividido** | RN 5 e RN 7 ficam na Agenda (P1.1 – Arrastar atividade); RN 6 vai para P6.2 – Remarcar OS inteira |
| [[P6.3 - Remarcar atividade|P1.3 - Remarcar atividade]] (RN 8) | P6.3 | |
| [[P6.4 - Editar OS inteira|P1.4 - Editar OS inteira]] (RN 9, 35) | P6.4 | |
| [[P6.5 - Verificar conflito de horário|P1.5 - Verificar conflito de horário]] (RN 10, 11) | P6.5 | |
| [[P6.6 - Concluir ou cancelar|P1.6 - Concluir ou cancelar]] (RN 12, 13) | P6.6 | |
| [[P6.7 - Excluir|P1.7 - Excluir]] (RN 14–16) | P6.7 | |
| [[P6.8 - Adicionar atividade a OS existente|P1.8 - Adicionar atividade a OS existente]] (RN 36) | P6.8 | |

## Entidades
- [[Ordem de Serviço]] e [[Atividade da OS]] passam para o módulo OS.
- A Agenda **fica sem entidade própria**: ela só lê e move as atividades das OS. Isso confirma que a Agenda é uma forma de ver as OS.

## Onde mais precisa mudar
- [x] [[Agenda]]: reduzir para os 12 RF
- [x] Criar `Módulos/Ordem de Serviço (módulo).md`
- [x] Renomear os arquivos RF 1.x e P1.x e criar os RF 6.x e P6.x
- [x] Corrigir as referências cruzadas: RF 1.15 → RF 1.25 (passa a ser RF 6.11 → RF 6.17); RN 9 → RN 14
- [x] [[RF 2.2]]: incluir "ordem de serviço" na lista de funcionalidades dos dois perfis
- [x] [[RF 5.8]]: verificar a referência à criação da OS
- [x] Domínio: [[Ordem de Serviço]], [[Atividade da OS]], [[Tipo de Atividade]], [[Cliente]], [[Endereço]] (linha "Módulos")
- [x] [[Backlog]]: itens 02 a 05 passam para o módulo OS (o 01 continua na Agenda)
- [x] [[Planejamento de Entregas]]: a entrega 1 passa a incluir a OS
- [x] [[Status da Implementação]], [[API REST]], [[Frontend]], [[Decisão - Datas e Horas como Texto]]: atualizar as referências
- [x] [[Diagrama de Contexto.canvas|Diagrama de Contexto]] e `00 - Visão Geral`: incluir o módulo OS
- [ ] Doc técnica V7 e [[Histórico de Versões]]

## Decisões
- Agenda renumerada de RF 1.1 a 1.12 (sem lacunas); o número da V6 fica na propriedade `id_v6` de cada RF.
- Sinalização de conflito: inteira na OS (RF 6.12); a Agenda só exibe o aviso.
- Distinção visual por status: continua na Agenda (RF 1.6).
- Nome do módulo: "Ordem de Serviço" (nota `Ordem de Serviço (módulo)`, seguindo o padrão de Orçamento).
- Pendente fora do vault: atualizar a Documentação Técnica (V7).
