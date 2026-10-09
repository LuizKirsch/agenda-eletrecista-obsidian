---
tags: [projeto]
atualizado: 2026-10-09
---
# Status da Implementação

Comparação entre a Documentação Técnica V6 e o código em `server/` (até o commit `50ef569`, 05/10/2026). Cada RF tem a propriedade `implementacao` (`completa`, `parcial` ou `pendente`), e a view **Implementação** de [[Requisitos.base|Requisitos]] lista os que faltam.

| Módulo | Completos | Parciais | Pendentes |
| --- | --- | --- | --- |
| [[Agenda]] | 12 | 0 | 0 |
| [[Ordem de Serviço (módulo)\|Ordem de Serviço]] | 16 | 3 | 0 |
| [[Atividade]] | 8 | 0 | 0 |
| [[Cliente e Endereço]] | 7 | 1 | 4 |
| [[Usuários e Acesso]] | 10 | 3 | 0 |
| [[Orçamento (módulo)\|Orçamento]] | 0 | 0 | 7 |

## Divergências com a doc V6

### Ordem de Serviço
- **Concluídas/canceladas editáveis na edição da OS** ([[RF 6.11]], [[RF 6.8]], [[P6.4 - Editar OS inteira#RN 9|RN 9]]): o `OsForm` carrega todas as atividades como linhas editáveis e removíveis, e `os.service.atualizar` atualiza ou apaga qualquer uma sem conferir o status. Além disso, `lerOs` não rejeita linhas com o mesmo `id`: a atividade é atualizada duas vezes e a sequência fica com buraco ([[P6.4 - Editar OS inteira#RN 35|RN 35]]).
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
- `cliente.telefone` sem UNIQUE.
- FKs sem `ON DELETE` explícito; a exclusão da OS apaga as atividades no service, não por cascata.
- `atividade_os.status` aceita NULL (tem só o DEFAULT `'agendada'`); uma linha com NULL escapa do filtro `status <> 'cancelada'` e fica fora da checagem de conflito ([[P6.5 - Verificar conflito de horário#RN 10|RN 10]]).
- `cliente.telefone` é NOT NULL, mas a anonimização apaga o telefone ([[P3.4 - Anonimizar cliente#RN 47|RN 47]]); ao criar o UNIQUE, a coluna precisa aceitar NULL. `cliente.anonimizado_em` ainda não existe.
- A migration de `usuario` cria a tabela e insere a secretária sem transação; se o insert falhar no MySQL, a tabela fica criada e o próximo `db:migrate` falha.

## Auditoria de 09/10/2026
Achados da auditoria do código (relatórios em `server/.cartographer/`) que ainda não estavam registrados acima. Nenhum foi corrigido.

### Usuários e Acesso
- **Autoproteção da secretária burlável** ([[P2.3 - Cadastrar, editar e excluir usuário#RN 31|RN 31]]): `ehOProprio` (`services/usuario.service.js:29`) compara o id cru da URL. Com `PUT` ou `DELETE /api/usuarios/01`, o `findByPk` encontra o id 1, mas a checagem não reconhece o próprio usuário, e a secretária consegue se excluir, se desativar ou trocar o próprio perfil.
- **Logout com sessão expirada** ([[RF 2.6]]): a rota exige sessão válida, então com o token expirado o cookie não é limpo.
- **Login sem limite de tentativas** ([[P2.1 - Autenticar|P2.1]]).

### Agenda e Ordem de Serviço
- **Grade de 15 minutos só no front** ([[P1.1 - Arrastar atividade#RN 7|RN 7]]): `ehHora` (`services/horario.js:29`) aceita qualquer minuto.
- **`GET /api/agenda` sem limite de período** ([[API REST]]): `controllers/agenda.controller.js:7` aceita qualquer intervalo e carrega todas as atividades com joins.
- **Corrida no carregamento da semana** ([[RF 1.1]]): `Agenda.jsx:25-33` não descarta respostas antigas; ao trocar de semana rápido, a resposta anterior pode sobrescrever a atual. Um erro de carga também nunca é limpo depois de um carregamento bem-sucedido.
- **Corrida no formulário da OS** ([[RF 6.1]]): os effects de endereços e observações em `OsForm.jsx:67-76` não descartam respostas antigas; ao trocar de cliente rápido, a lista pode mostrar endereços do cliente anterior. A API recusa o envio, porque confere se o endereço pertence ao cliente.

### Atividade
- **Nome único sem diferenciar maiúsculas só no MySQL** ([[P5.1 - Gerenciar tipos de atividade#RN 17|RN 17]]): a comparação depende da collation; no SQLite de desenvolvimento, "Instalação" e "instalação" passam. O mesmo vale para o `login` do usuário.

### Código e configuração
- `config/config.js:17` usa a mesma configuração para `development`, `test` e `production`.
- Comentários no front citam a numeração V6 dos RFs (`Agenda.jsx:35,54,72`, `Grade.jsx:35`, `OsForm.jsx:7,15`).

## Limpeza no repositório
- Os arquivos vazios `agenda-eletricista-server@0.1.0`, `concurrently`, `dev` e `vite` na raiz do `server/` entraram no commit `8c0c06f` (sobra de um comando npm digitado errado) e podem ser removidos.
- O commit `8c0c06f` alterou a migration de `tipo_atividade`, que já existia, para suportar SQLite. Bancos MySQL já migrados não são afetados, porque o SQL gerado para MySQL é o mesmo.

Ver também: [[Histórico de Commits]], [[API REST]], [[Frontend]]
