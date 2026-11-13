---
tags: [projeto]
atualizado: 2026-11-13
---
# Status da Implementação

Comparação entre a Documentação Técnica V6 e o código em `server/` (até o commit `d4f00e4`, 06/11/2026). Cada RF tem a propriedade `implementacao` (`completa`, `parcial` ou `pendente`), e a view **Implementação** de [[Requisitos.base|Requisitos]] lista os que faltam.

| Módulo | Completos | Parciais | Pendentes |
| --- | --- | --- | --- |
| [[Agenda]] | 14 | 0 | 0 |
| [[Ordem de Serviço (módulo)\|Ordem de Serviço]] | 23 | 0 | 0 |
| [[Atividade]] | 8 | 0 | 0 |
| [[Cliente e Endereço]] | 13 | 0 | 0 |
| [[Usuários e Acesso]] | 14 | 0 | 0 |
| [[Orçamento (módulo)\|Orçamento]] | 20 | 0 | 0 |

Todos os RFs estão implementados, exceto o [[RF 4.21]] (deslocamento por geolocalização na recomendação), que ficou fora do escopo em 13/11/2026 ([[Fora do MVP]]). O [[RF 4.19]] (recomendação de horários) e o [[RF 4.13]] foram concluídos em 06/11/2026. A [[P4.2 - Aceitar ou recusar orçamento#RN 68|RN 68]] também: com conflito no confirmar, a API recusa (409, `codigo: conflito`) e a tela oferece recalcular ou gerar a OS mesmo assim. O [[RF 6.23]] (exportar OS em PDF) foi criado e implementado em 06/11/2026.

## Entrega de 06/11/2026
Feita em quatro frentes paralelas e juntada na `main` no commit `d4f00e4`; migrations aplicadas no `dev.sqlite` (backup em `dev.sqlite.antes-rfs-2026-11-06.bak`).
- **Eletricista por OS e por atividade**: [[RF 6.21]], [[RF 6.22]], [[RF 1.13]], [[RF 1.14]], [[RF 6.19]], [[RF 6.12]], [[RF 2.14]] e a escolha do eletricista no aceite ([[RF 4.13]]). Migration `20261106000100-add-eletricista-os-atividade.js`.
- **Permissões, telefone e tipos**: [[RF 2.2]], [[RF 2.3]], [[RF 2.9]], [[RF 2.11]], [[RF 3.1]], [[RF 3.9]], [[RF 5.6]]. Sem migration.
- **Cliente e endereço nos formulários**: [[RF 6.1]], [[RF 6.2]], [[RF 4.17]] (componente `SeletorClienteEndereco`). Sem migration.
- **Orçamento**: [[RF 4.18]] (PDF pela impressão do navegador) e [[RF 4.20]] ([[Versão do Orçamento]], migration `20261106000400-create-orcamento-versao.js`).
- Teste integrado da API numa cópia do banco: 25 de 25 checagens. As telas só passaram pelo build; não foram abertas no navegador.
- Decisões que precisam de aval: as OS antigas receberam o primeiro eletricista cadastrado (no `dev.sqlite`, o Edson, que está inativo); remarcar ou arrastar não troca o eletricista; trocar o perfil de um eletricista com vínculos não é bloqueado.

## Divergências com a doc V6

### Ordem de Serviço
- **Endereço opcional na OS** ([[RF 6.1]], [[P6.1 - Criar OS#RN 34|RN 34]]): resolvido na API em 06/11/2026; a coluna continua aceitando NULL (ver "Diferenças no banco").
- **Concluídas/canceladas editáveis na edição da OS** ([[RF 6.11]], [[RF 6.8]], [[P6.4 - Editar OS inteira#RN 9|RN 9]]): resolvido em 27/10/2026. O `OsForm` mostra essas atividades só para leitura e `os.service.atualizar` recusa removê-las (409) e ignora alterações nelas, mantendo só a renumeração da sequência; linhas com o mesmo `id` são recusadas (400).
- **Busca e cadastro rápido no formulário da OS** ([[RF 6.2]]): resolvido em 06/11/2026.

### Usuários e Acesso
- **Cadastro de usuário liberado ao eletricista** ([[RF 2.9]], [[P2.3 - Cadastrar, editar e excluir usuário#RN 29|RN 29]]): resolvido em 06/11/2026.

### Cliente e Endereço
- **Telefone** ([[RF 3.1]], [[P3.1 - Cadastrar cliente, endereço e observação#RN 37|RN 37]]): validação e máscara resolvidas em 06/11/2026; a coluna `cliente.telefone` ainda não é UNIQUE.
- **Editar e excluir** ([[RF 3.9]] a [[RF 3.12]], [[P3.3 - Editar e excluir cliente, endereço e observação|P3.3]]): implementado em 27/10/2026. As FKs continuam sem `ON DELETE CASCADE`; a cascata da [[P3.3 - Editar e excluir cliente, endereço e observação#RN 43|RN 43]] é feita nos services. A edição passou a validar o telefone em 06/11/2026 ([[RF 3.9]]).
- **Busca sem acento no SQLite** ([[RF 3.8]]): no MySQL a collation padrão ignora acentos; no SQLite de desenvolvimento, não.

### Atividade e Orçamento (decisões de 19/10/2026)
- **Tipo nunca é excluído** ([[RF 5.6]], [[P5.1 - Gerenciar tipos de atividade#RN 19|RN 19]]): resolvido em 06/11/2026; a exclusão saiu da API e da tela.
- Resolvidos em 27/10/2026: valor padrão do tipo e uso em orçamentos ([[RF 5.1]] a [[RF 5.3]], [[RF 5.5]], [[RF 5.7]]) e atividade avulsa na OS ([[RF 6.3]], [[RF 6.4]]).

### Validação das RFs e RNs (27/10/2026)
Detalhes em [[Validação de RFs e RNs]].
- Furos corrigidos nas regras e no código: orçamento não bloqueia mais a exclusão de cliente/endereço e é excluído junto ([[P3.3 - Editar e excluir cliente, endereço e observação#RN 42|RN 42]], [[P3.3 - Editar e excluir cliente, endereço e observação#RN 43|RN 43]]); OS vinda de orçamento não troca de cliente ([[P6.4 - Editar OS inteira#RN 57|RN 57]]); o aceite do orçamento gera OS em vários dias ([[P4.2 - Aceitar ou recusar orçamento#RN 51|RN 51]], revisto em 28/10/2026); a RN 21 vale só para a criação manual de OS.
- Decisões registradas como RN, sem mudança de código: [[P4.2 - Aceitar ou recusar orçamento#RN 56|RN 56]], [[P6.4 - Editar OS inteira#RN 58|RN 58]], [[P6.6 - Concluir ou cancelar#RN 59|RN 59]], [[P6.1 - Criar OS#RN 60|RN 60]], [[P3.3 - Editar e excluir cliente, endereço e observação#RN 61|RN 61]].
- [[RF 1.5]] reescrito para o menu principal; [[RF 3.13]] já estava implementado.

### Orçamento
- Implementado em 27/10/2026 (`orcamento.service`, telas `/orcamentos`). O vínculo com a OS só nasce do aceite; vincular um orçamento a uma OS já existente ([[RF 4.7]], caminho citado na [[Proposta - Modelo do Orçamento]]) não tem tela.
- Excluir a OS gerada não apaga o orçamento: `orcamento.ordem_servico_id` tem `ON DELETE SET NULL`, e o orçamento continua aceito, sem OS.
- A migration altera `atividade_os` e `tipo_atividade`; no SQLite isso recria as tabelas, e a migration restaura o CHECK e o índice de `atividade_os`.

## Diferenças no banco
Ver a seção "Implementação" de cada entidade em `Domínio/`.
- `cliente.telefone` sem UNIQUE; a unicidade é conferida no service. Antes do índice, limpar os 3 clientes de teste com `519999999956`.
- FKs sem `ON DELETE` explícito; a exclusão da OS apaga as atividades no service, não por cascata.
- Resolvido em 13/11/2026 (migration `20261113000100-not-null-os-atividade.js`, commit `6ab82a9`): `atividade_os.status` ([[P6.5 - Verificar conflito de horário#RN 10|RN 10]]), `ordem_servico.endereco_id` ([[RF 6.1]]), `ordem_servico.eletricista_id` ([[RF 6.21]]) e `atividade_os.eletricista_id` ([[RF 6.22]]) passaram a NOT NULL; status NULL vira `'agendada'`, e a migration aborta se houver endereço ou eletricista NULL. Aplicada no `dev.sqlite` (backup em `dev.sqlite.antes-notnull-2026-11-13.bak`). No SQLite, a recriação da tabela tirou o `AUTOINCREMENT` de `ordem_servico.id` (o id da última OS excluída pode ser reaproveitado); no MySQL não muda.
- O `down` da migration `20261106000100` falha no SQLite (`removeColumn` com FK); no MySQL não foi testado.
- A migration de `usuario` cria a tabela e insere a secretária sem transação; se o insert falhar no MySQL, a tabela fica criada e o próximo `db:migrate` falha.

## Auditoria de 09/10/2026
Achados da auditoria do código (relatórios em `server/.cartographer/`) que ainda não estavam registrados acima. Os de Usuários e Acesso e as corridas de carregamento foram corrigidos em 13/11/2026 (commit `6ab82a9`); os demais seguem abertos.

### Usuários e Acesso
- **Autoproteção da secretária burlável** ([[P2.3 - Cadastrar, editar e excluir usuário#RN 31|RN 31]]): resolvido em 13/11/2026. O `usuario.controller` normaliza o id da URL com `lerId`, então `/api/usuarios/01` vira o id 1 e a checagem do próprio usuário funciona.
- **Logout com sessão expirada** ([[RF 2.6]]): resolvido em 13/11/2026. A rota de logout não exige mais sessão válida e sempre limpa o cookie.
- **Login sem limite de tentativas** ([[P2.1 - Autenticar|P2.1]]): resolvido em 13/11/2026. Depois de 5 falhas em 15 minutos para o mesmo login e IP, a API responde 429; a mensagem de erro do login continua genérica ([[P2.1 - Autenticar#RN 22|RN 22]]). O controle fica em memória (zera ao reiniciar o servidor), e o app usa `trust proxy` para ler o IP real atrás do Caddy.

### Agenda e Ordem de Serviço
- **Grade de 15 minutos só no front** ([[P1.1 - Arrastar atividade#RN 7|RN 7]]): `ehHora` (`services/horario.js:29`) aceita qualquer minuto.
- **`GET /api/agenda` sem limite de período** ([[API REST]]): `controllers/agenda.controller.js:7` aceita qualquer intervalo e carrega todas as atividades com joins.
- **Corrida no carregamento da semana** ([[RF 1.1]]): resolvido em 13/11/2026. `Agenda.jsx` só aplica a resposta da última chamada e limpa o erro depois de um carregamento bem-sucedido.
- **Corrida no formulário da OS** ([[RF 6.1]]): resolvido em 13/11/2026. A busca de cliente e endereço (`SeletorClienteEndereco`) já descartava respostas antigas; o effect das observações do endereço em `OsForm.jsx` passou a descartar também.

### Atividade
- **Nome único sem diferenciar maiúsculas só no MySQL** ([[P5.1 - Gerenciar tipos de atividade#RN 17|RN 17]]): a comparação depende da collation; no SQLite de desenvolvimento, "Instalação" e "instalação" passam. O mesmo vale para o `login` do usuário.

### Código e configuração
- `config/config.js:17` usa a mesma configuração para `development`, `test` e `production`.
- Comentários no front citam a numeração V6 dos RFs (`Agenda.jsx:35,54,72`, `Grade.jsx:35`, `OsForm.jsx:7,15`).

## Limpeza no repositório
- Os arquivos vazios `agenda-eletricista-server@0.1.0`, `concurrently`, `dev` e `vite` na raiz do `server/` entraram no commit `8c0c06f` (sobra de um comando npm digitado errado) e podem ser removidos.
- O commit `8c0c06f` alterou a migration de `tipo_atividade`, que já existia, para suportar SQLite. Bancos MySQL já migrados não são afetados, porque o SQL gerado para MySQL é o mesmo.

Ver também: [[Histórico de Commits]], [[API REST]], [[Frontend]]
