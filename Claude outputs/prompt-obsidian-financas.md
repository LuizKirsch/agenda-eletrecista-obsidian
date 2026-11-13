# Prompt: criar o vault Obsidian do app de finanças

Cole o texto abaixo (a partir de "Quero que você...") numa sessão do Claude Code aberta na pasta do novo vault, ou numa sessão do Cowork com a pasta conectada.

---

Quero que você crie o vault do Obsidian de documentação de um app de controle da minha vida financeira pessoal. Esse vault deve seguir a mesma estrutura e as mesmas convenções que usei no vault do projeto Agenda do Eletricista (RFs, RNs, módulos, domínio, arquitetura, decisões etc.). Não quero código do app agora, só a documentação estruturada.

## Contexto do app

- App pessoal, só para mim (usuário único no início).
- Ideia central: mando os gastos por um bot no Telegram, um agente de IA interpreta e organiza (valor, categoria, data, forma de pagamento), e eu vejo relatórios e faço perguntas ("quanto gastei com mercado em outubro?") numa interface web.
- Pensei em FastAPI no back e React no front, em monolito modular (módulos no mesmo código, sem microserviços). Trate isso como proposta, não como decisão fechada. Se achar que outra stack combina mais, registre como decisão em discussão.
- Vou documentar como no projeto da agenda: primeiro o modelo, depois os requisitos, e só então o código.

## O que quero que você replique do vault da agenda

Estrutura de pastas na raiz:

- `00 - Visão Geral.md`: índice com links para tudo (projeto, módulos, domínio, requisitos, regras de negócio, arquitetura).
- `README.md`: tabela de pastas e como abrir o vault.
- `Projeto/`: Contexto, Planejamento de Entregas, Backlog, Histórico de Versões, Status da Implementação, Fora do MVP, Pendências.
- `Módulos/`: um índice por módulo, com resumo, entidades, processos/RNs, lista de RFs com prioridade e uma linha de texto, e link de volta para a Visão Geral.
- `Requisitos/<Módulo>/RF X.Y.md`: um RF por nota, com o frontmatter abaixo, e um `Requisitos.base` (tabela filtrável por módulo, prioridade, entrega e implementação).
- `Regras de Negócio/P<módulo>.<n> - <Processo>.md`: um processo por nota, com as RNs como seções `### RN n`, linkando as RNs entre processos quando uma referencia a outra.
- `Domínio/`: uma nota por entidade, com tabela, módulos, relacionamentos (1 → N) e dicionário de dados (nome, descrição, tipo, tamanho, restrições).
- `Arquitetura/`: Stack e Ambiente, Requisitos Não Funcionais, API REST, Frontend e uma nota `Decisão - <título>.md` por decisão.
- `Diagramas/`: Canvas do Mapa do Domínio e do Diagrama de Contexto (arquivos `.canvas`), mais uma pasta para BPMN/sequência quando eu pedir.
- `Telas/`: vazia por enquanto, só com uma nota explicando para que serve.
- `Templates/`: `Requisito.md`, `Decisão.md` e um template de Regra de Negócio/Processo.
- `.gitignore` igual ao do vault da agenda (ignora `workspace.json`, `workspace-mobile.json`, cache, `.trash/`, `.DS_Store`, `Thumbs.db`) e a configuração mínima de `.obsidian`.

Frontmatter dos RFs:

```yaml
---
tags: [requisito]
id: "RF 1.1"
modulo: "[[Nome do Módulo]]"
prioridade: Alta | Média | Baixa
alterado: false
entrega: 1
implementacao: pendente
---
```

Corpo do RF: o texto do requisito em uma frase ("O sistema deve..."), depois `**Módulo:**` e `**Entidades:**` com wikilinks, e uma linha de fonte no final.

Frontmatter de módulo: `tags: [modulo]` e `entrega`. De entidade: `tags: [entidade]` e `tabela`. De processo: `tags: [processo]`, `processo`, `modulo`, `execucao` (Usuário, Sistema ou Usuário e sistema). De decisão: `tags: [decisao]` e `status` (proposta, aceita, rejeitada).

## Convenções que precisam ser mantidas

1. A numeração dos RFs é por módulo, não sequencial global: RF 1.x é o primeiro módulo, RF 2.x o segundo, e assim por diante. Nunca deduza um RF pelo número do backlog.
2. As RNs têm numeração global contínua (RN 1, RN 2, ...) e ficam dentro dos processos. Não renumere depois que existirem, para manter a rastreabilidade.
3. Todo link entre notas é wikilink. Cada RF aponta para seu módulo e suas entidades, e cada módulo lista seus RFs.
4. Não invente dados. Se uma informação não foi definida por mim, escreva "a definir" ou coloque em `Projeto/Pendências.md`. Nunca preencha com suposição apresentada como fato.
5. Coisas que eu decidir ficam em `Decisão - ...` com data, contexto, decisão, justificativa e consequências. Coisas em discussão entram com `status: proposta`.
6. Tudo em português do Brasil. Escreva de forma natural, sem rótulos de texto genérico e sem floreio.
7. Dados financeiros reais meus (valores, saldos, contas, números de cartão) não entram no vault. Só exemplos fictícios, e marcados como exemplo.

## Como quero que você trabalhe

Faça em etapas e pare para eu validar entre elas.

**Etapa 1: perguntas.** Antes de criar qualquer arquivo, me faça no máximo 6 perguntas objetivas, em múltipla escolha quando der, sobre o que muda a estrutura. Sugestões do que perguntar: se haverá mais de um usuário no futuro (ex.: casal), quais contas/meios de pagamento entram (dinheiro, cartão de crédito, Pix, conta corrente), se entram receitas além de gastos, se entram orçamento mensal por categoria, metas e gastos recorrentes/parcelados, e se o agente de IA só registra ou também responde perguntas.

**Etapa 2: proposta de módulos.** Com as respostas, proponha a lista de módulos (por exemplo: Registro de Gastos via Telegram, Categorias, Contas e Cartões, Relatórios, Agente de IA, Orçamento e Metas, Usuários e Acesso), com uma frase de escopo cada, o que fica no MVP e o que vai para "Fora do MVP". Espere eu aprovar.

**Etapa 3: esqueleto do vault.** Crie toda a estrutura de pastas, README, Visão Geral, templates, .gitignore, notas de módulo, o Diagrama de Contexto e o Mapa do Domínio em `.canvas`, as entidades com dicionário de dados e os primeiros RFs e processos de cada módulo do MVP. Use `implementacao: pendente` em tudo. Me mostre um resumo do que criou (quantos RFs, RNs, entidades) e uma lista do que ficou como "a definir".

**Etapa 4: validação.** Faça uma varredura final conferindo que todo wikilink resolve, que nenhum RF ficou sem módulo, que as RNs referenciadas existem, que o `Requisitos.base` lista todos os RFs e que a Visão Geral aponta para todas as notas. Corrija o que achar e relate o que corrigiu.

Ao final, inicialize o repositório git e faça o commit inicial, mas não faça push.
