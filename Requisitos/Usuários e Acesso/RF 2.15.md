---
tags: [requisito]
id: "RF 2.15"
modulo: "[[Usuários e Acesso]]"
prioridade: Média
alterado: false
entrega: 3
implementacao: completa
---
# RF 2.15

o sistema deve permitir que qualquer usuário escolha o tamanho das letras da interface entre pequena, média, grande e extra grande, a partir do menu principal; a escolha vale para todas as telas, fica salva no aparelho em que foi feita e a média é o padrão (decisão do projeto);

**Módulo:** [[Usuários e Acesso]]
**Entidades:** —
**Implementação:** `client/src/fonte.js` guarda a escolha no `localStorage` (`tamanhoFonte`) e aplica a variável CSS `--fonte` (pequena 0,9, média 1, grande 1,2, extra grande 1,5); todos os `font-size` do `estilo.css` e os inline usam `calc(Npx * var(--fonte))`, então só o texto muda, não o layout da agenda. Seletor "Tamanho da letra" no menu lateral (computador) e no menu da conta (celular). Campos de formulário no celular nunca ficam abaixo de 16px, para o iPhone não dar zoom. A impressão da OS sai sempre no tamanho normal (13/11/2026).
**Regras:** —

> Origem: pedido dos usuários em 13/11/2026; no celular as letras ficaram pequenas demais.
> Extra grande (150%) incluído a pedido do Luiz em 13/11/2026.
> Salvo no aparelho, e não no cadastro do usuário, para que a mesma pessoa possa usar letra grande no celular e média no computador.
