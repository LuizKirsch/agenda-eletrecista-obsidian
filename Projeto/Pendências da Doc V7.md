---
tags: [projeto]
atualizado: 2026-11-11
---
# Pendências da Doc V7

Versão atual: `Claude outputs/Documentacao_Tomada_de_Decisao_v7_3.docx` (e `.pdf`), layout do modelo IENH. Histórico: V2 a V7, com a V7 em 11/11/2026.

## Seções da doc
- [ ] **Seção 10 – Protótipos**: os prints são de 28/10/2026 e não mostram o que entrou em 06/11: eletricista por atividade, cor do eletricista na agenda, filtro com seleção múltipla ([[RF 1.13]]) e botão "Exportar PDF" da OS ([[RF 6.23]]). Precisa de prints novos do sistema.

## Fora da doc
- [ ] [[RF 4.21]] (deslocamento por geolocalização) fica fora da doc: não faz sentido para a V1 do sistema (decisão de 11/11/2026); reavaliar depois da análise.
- [ ] Backlog (planilha): RF 4.8 a 4.15, mudanças de Atividade e título do item 10; conferir também os RFs de 28/10 e 06/11 (RF 1.13, 1.14, 2.14, 4.16 a 4.20, 6.21 a 6.23; o RF 4.21 fica fora da V1).
- [ ] Subir a v7_3 no projeto do Claude (lá ainda está a v6_1).
- [ ] Commit do vault.
- [ ] Apagar `Claude outputs/_to_delete` (imagens de conferência, v8 e versão 09-11-2026).

## Código
- [ ] `POST /usuarios` no `main` ainda sem `somenteSecretaria` ([[RF 2.9]]); a correção de 06/11 precisa subir para o GitHub.
- [ ] Divergências em [[Status da Implementação]] (ex.: `endereco_id` e `eletricista_id` sem NOT NULL no banco, garantidos pela API).

## Feitas
- [x] Seções 1 a 6, 8, 10 e 11 (até 28/10/2026).
- [x] (11/11) Seção 3: infraestrutura com Docker e Caddy ([[Decisão - Deploy com Docker e Caddy]]).
- [x] (11/11) Seções 4 e 6: [[RF 6.23]] incluído e [[RF 1.13]] com seleção múltipla.
- [x] (11/11) Seção 7: RN 7, RN 9, RN 36, RN 67 e RN 68 iguais ao vault; frase sobre a numeração das RN e índice RN → processo no fim da seção; BPMN P2.3, P4.1, P4.2, P6.1, P6.4, P6.5, P6.7 e P6.8 atualizados (eletricista, recomendação de horários, OS encerrada só leitura, RN 56, 64, 65 e 66).
- [x] (11/11) Seção 9: sequência de Criar OS com eletricista (RN 62, 63 e conflito por eletricista), sem mudar a numeração dos passos.
- [x] (11/11) Seção 12: componentes – visão geral, Criar OS, Aceitar orçamento e Autenticar (`Claude outputs/Diagramas 12 e 13`).
- [x] (11/11) Seção 13: classes – visão geral, Criar OS e Aceitar orçamento.
- [x] (11/11) Seções 14 e 15: DER e dicionário com `eletricista_id` (OS e atividade), `usuario.cor` e `orcamento_versao`.
- [x] (11/11) Seção 7: P6.2 começa na escolha "OS inteira" do P1.1 (sem repetir RN 5 e a pergunta); P6.1 com 2 raias (Usuário e Sistema); coluna Execução padronizada: "Usuário e sistema", "Secretária e sistema" (2.2 e 2.3) e "Sistema" (2.4).
- [x] (11/11) Capa: nome do projeto trocado para **Prestô**.
- [x] (11/11) Histórico: linha da V1 removida e V7 com data de 11/11/2026.
