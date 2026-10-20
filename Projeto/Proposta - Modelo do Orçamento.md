---
tags: [projeto, proposta]
status: decidida
data: 2026-10-19
versao_alvo: V7
---
# Proposta – Modelo de dados do Orçamento

Fecha o banco de dados e o dicionário de dados do módulo [[Orçamento (módulo)|Orçamento]] (entrega 2).

## Premissas
- No orçamento é possível adicionar **atividades já existentes** (catálogo de [[Tipo de Atividade]]).
- É possível criar **atividades só para aquele orçamento** (avulsas), que não entram no catálogo.
- O **preço pode ser alterado** em cada orçamento sem mudar o preço do catálogo.

## Decisões
- **O catálogo do orçamento é o próprio [[Tipo de Atividade]].** Não há catálogo próprio de itens; `tipo_atividade` ganha a coluna `valor_padrao`.
- **Item de serviço é a atividade vinculada ao orçamento** (decisão de 19/10/2026). Uma tabela só para os itens ([[Item de Serviço]], `orcamento_item`): atividade do catálogo tem `tipo_atividade_id` preenchido; atividade avulsa tem `tipo_atividade_id = NULL` e nunca vai para o catálogo ([[RF 4.5]], [[RF 4.6]]).
- **Preço copiado.** Ao adicionar uma atividade do catálogo, `valor_padrao` é copiado para `valor_unitario`, que pode ser editado. Alterar o valor no orçamento não muda o catálogo e reajustar o catálogo não muda orçamentos antigos ([[RF 4.3]], [[RF 4.4]]).
- **Descrição copiada.** O nome da atividade é copiado para `descricao`; renomear o tipo não altera um orçamento já passado ao cliente.
- **FK no orçamento, não na OS.** `orcamento.ordem_servico_id` (NULL, UNIQUE) atende os dois caminhos: orçamento criado a partir de uma OS e orçamento que vem antes e gera a OS ao ser aprovado. Garante 0..1 orçamento por OS ([[RF 4.7]]) e não muda a tabela `ordem_servico`.
- **Total calculado**, não armazenado: soma de `quantidade × valor_unitario` dos itens.

## Tabelas
- `tipo_atividade` — nova coluna `valor_padrao` ([[Tipo de Atividade]])
- `orcamento` — nova ([[Orçamento]])
- `orcamento_item` — nova ([[Item de Serviço]])

## Decisões de 19/10/2026
1. **Atividade avulsa na OS.** Ao aceitar o orçamento, o item avulso vira uma atividade avulsa na própria `atividade_os`: `tipo_atividade_id` passa a aceitar NULL e entra a coluna `descricao` ([[Atividade da OS]]). Nenhuma regra da OS muda.
2. **Quantidade e tempo.** A quantidade é a de cada atividade do orçamento (`orcamento_item.quantidade`, padrão 1); o total é a soma de `quantidade × valor_unitario`. Cada item vira **uma única atividade** na OS. O tempo do item fica em `orcamento_item.duracao_min`: sugerido como `quantidade × duração padrão do tipo` e editável (ex.: 10 tomadas × 15 min = 2h30, ajustado para 1h30). No item avulso, o tempo é informado à mão. Na OS, o fim da atividade é calculado pelo `duracao_min` do item e continua ajustável ([[RF 6.4]]).
3. **Status.** `pendente`, `aceito` e `recusado`, padrão `pendente`; sem data de validade e sem desconto. O orçamento aceito é o que vira OS.
4. **Tipo desativado** ([[RF 5.5]]). Desativar faz o tipo sumir das opções, sem apagar. Não é oferecido em orçamentos novos, mas permanece nos que já o usam. Um orçamento já enviado com tipo desativado é aceito normalmente e a atividade entra na OS, porque o orçamento já foi passado ao cliente; o tipo só não pode mais ser usado em OS ou orçamentos novos. A contagem de uso ([[RF 5.7]]) e o bloqueio de exclusão ([[RF 5.6]], [[P5.1 - Gerenciar tipos de atividade#RN 19|RN 19]]) passam a considerar também `orcamento_item`.

## Ajustes de texto a levar para a doc

> **Aplicados no vault em 19/10/2026** (RF 4.1 a 4.15, RF 5.1 a 5.7, RF 6.3, RF 6.4, P4.1 a P4.3, P5.1) e levados ao rascunho da doc V7 em 19/10/2026.

- O termo "item de serviço" continua: é a atividade vinculada ao orçamento. [[RF 4.3]] a [[RF 4.6]] não mudam de termo.
- [[RF 4.1]], [[RF 4.2]]: o catálogo deixa de ser de itens de serviço e passa a ser o de tipos de atividade com valor padrão; o item de serviço é criado no orçamento a partir de um tipo ou como avulso.
- [[RF 5.1]], [[RF 5.2]], [[RF 5.3]]: incluir o valor padrão no cadastro e na edição do tipo.
- [[RF 5.6]], [[RF 5.7]], [[P5.1 - Gerenciar tipos de atividade#RN 19|RN 19]]: considerar o uso em orçamentos.
- Backlog item 10 ("Catálogo de itens de serviço"): o catálogo passa a ser o de tipos de atividade.
- [[RF 6.3]]: a atividade da OS passa a ter tipo **ou** descrição (avulsa).
- [[RF 6.4]]: na atividade vinda do orçamento, o fim é sugerido pelo tempo do item, não pela duração padrão do tipo.
- [[RF 5.5]]: o tipo inativo também não é oferecido em orçamentos novos, mas o orçamento já enviado continua valendo.
- Novos RFs do Orçamento (RF 4.8 em diante): status, quantidade e tempo do item, total calculado e conversão do orçamento aceito em OS.
