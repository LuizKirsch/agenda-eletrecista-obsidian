---
tags: [projeto]
atualizado: 2026-10-05
---
# Status da Implementação

Comparação entre a Documentação Técnica V6 e o código em `server/` (até o commit `50ef569`, 05/10/2026). Cada RF tem a propriedade `implementacao` (`completa`, `parcial` ou `pendente`), e a view **Implementação** de [[Requisitos.base|Requisitos]] lista os que faltam.

| Módulo | Completos | Parciais | Pendentes |
| --- | --- | --- | --- |
| [[Agenda]] | 12 | 0 | 0 |
| [[Ordem de Serviço (módulo)\|Ordem de Serviço]] | 15 | 4 | 0 |
| [[Atividade]] | 8 | 0 | 0 |
| [[Cliente e Endereço]] | 7 | 1 | 4 |
| [[Usuários e Acesso]] | 10 | 3 | 0 |
| [[Orçamento (módulo)\|Orçamento]] | 0 | 0 | 7 |

## Divergências com a doc V6

### Ordem de Serviço
- **Endereço opcional na OS** ([[RF 6.1]], [[P6.1 - Criar OS#RN 34|RN 34]]): o formulário oferece "Sem endereço", `lerOs` aceita `endereco_id` nulo e a migration de `ordem_servico` deixa a coluna sem NOT NULL.
- **Concluídas/canceladas editáveis na edição da OS** ([[RF 6.11]], [[RF 6.8]], [[P6.4 - Editar OS inteira#RN 9|RN 9]]): o `OsForm` carrega todas as atividades como linhas editáveis e removíveis, e `os.service.atualizar` atualiza ou apaga qualquer uma sem conferir o status.
- **Busca e cadastro rápido no formulário da OS** ([[RF 6.2]]): o cliente é escolhido em um `<select>` com a lista inteira, sem busca e sem cadastro inline de cliente ou endereço.

### Usuários e Acesso
- **Cadastro de usuário liberado ao eletricista** ([[RF 2.9]], [[P2.3 - Cadastrar, editar e excluir usuário#RN 29|RN 29]]): `routes/usuario.routes.js` aplica `somenteSecretaria` só em PUT e DELETE; o POST e o formulário da tela ficam abertos aos dois perfis.

### Cliente e Endereço
- **Telefone** ([[RF 3.1]], [[P3.1 - Cadastrar cliente, endereço e observação#RN 37|RN 37]]): não há validação de DDD + 8/9 dígitos nem máscara, e a coluna `cliente.telefone` não é UNIQUE.
- **Editar e excluir** ([[RF 3.9]] a [[RF 3.12]], [[P3.3 - Editar e excluir cliente, endereço e observação|P3.3]]): ainda não existem rotas nem telas. As FKs de `endereco` e `endereco_observacao` foram criadas sem `ON DELETE CASCADE` ([[P3.3 - Editar e excluir cliente, endereço e observação#RN 43|RN 43]]).
- **Busca sem acento no SQLite** ([[RF 3.8]]): no MySQL a collation padrão ignora acentos; no SQLite de desenvolvimento, não.

### Orçamento
- Entrega 2, ainda sem tabelas, rotas ou telas.

## Diferenças no banco
Ver a seção "Implementação" de cada entidade em `Domínio/`.
- `ordem_servico.endereco_id` aceita NULL (doc: NOT NULL).
- `cliente.telefone` sem UNIQUE.
- FKs sem `ON DELETE` explícito; a exclusão da OS apaga as atividades no service, não por cascata.
- `atividade_os.status` aceita NULL (tem só o DEFAULT `'agendada'`).

## Limpeza no repositório
- Os arquivos vazios `agenda-eletricista-server@0.1.0`, `concurrently`, `dev` e `vite` na raiz do `server/` entraram no commit `8c0c06f` (sobra de um comando npm digitado errado) e podem ser removidos.
- O commit `8c0c06f` alterou a migration de `tipo_atividade`, que já existia, para suportar SQLite. Bancos MySQL já migrados não são afetados, porque o SQL gerado para MySQL é o mesmo.

Ver também: [[Histórico de Commits]], [[API REST]], [[Frontend]]
