---
tags: [projeto, proposta]
status: em discussão
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
- **O catálogo do orçamento é o próprio [[Tipo de Atividade]].** A entidade [[Item de Serviço]] deixa de existir; `tipo_atividade` ganha a coluna `valor_padrao`.
- **Uma tabela só para os itens** ([[Item do Orçamento]]): atividade do catálogo tem `tipo_atividade_id` preenchido; atividade avulsa tem `tipo_atividade_id = NULL` e nunca vai para o catálogo ([[RF 4.5]], [[RF 4.6]]).
- **Preço copiado.** Ao adicionar uma atividade do catálogo, `valor_padrao` é copiado para `valor_unitario`, que pode ser editado. Alterar o valor no orçamento não muda o catálogo e reajustar o catálogo não muda orçamentos antigos ([[RF 4.3]], [[RF 4.4]]).
- **Descrição copiada.** O nome da atividade é copiado para `descricao`; renomear o tipo não altera um orçamento já passado ao cliente.
- **FK no orçamento, não na OS.** `orcamento.ordem_servico_id` (NULL, UNIQUE) atende os dois caminhos: orçamento criado a partir de uma OS e orçamento que vem antes e gera a OS ao ser aprovado. Garante 0..1 orçamento por OS ([[RF 4.7]]) e não muda a tabela `ordem_servico`.
- **Total calculado**, não armazenado: soma de `quantidade × valor_unitario` dos itens.

## Tabelas
- `tipo_atividade` — nova coluna `valor_padrao` ([[Tipo de Atividade]])
- `orcamento` — nova ([[Orçamento]])
- `orcamento_item` — nova ([[Item do Orçamento]])

## Pendências
1. **Atividade avulsa ao virar OS.** `atividade_os.tipo_atividade_id` é NOT NULL. Na aprovação, a avulsa fica só no orçamento ou a secretária escolhe um tipo para ela?
2. **Quantidade.** Faz sentido para o Edson (ex.: instalar tomada × 5) ou cada linha é sempre uma unidade?
3. **Status e validade.** `aberto`, `aprovado` e `recusado` bastam? Precisa de data de validade ou desconto?
4. **Tipo desativado.** Não é oferecido em orçamentos novos, mas permanece nos antigos. A contagem de uso ([[RF 5.7]]) e o bloqueio de exclusão ([[RF 5.6]], [[P5.1 - Gerenciar tipos de atividade#RN 19|RN 19]]) passam a considerar também `orcamento_item`.

## Ajustes de texto a levar para a doc
- [[RF 4.1]], [[RF 4.2]]: trocar "item de serviço" por "tipo de atividade com valor padrão".
- [[RF 4.3]], [[RF 4.5]], [[RF 4.6]]: trocar "item" por "atividade".
- [[RF 5.1]], [[RF 5.2]], [[RF 5.3]]: incluir o valor padrão no cadastro e na edição do tipo.
- [[RF 5.6]], [[RF 5.7]], [[P5.1 - Gerenciar tipos de atividade#RN 19|RN 19]]: considerar o uso em orçamentos.
- Backlog itens 10 a 12: títulos citam "itens de serviço".
