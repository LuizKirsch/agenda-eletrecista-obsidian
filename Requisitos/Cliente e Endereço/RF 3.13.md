---
tags: [requisito, lgpd]
id: "RF 3.13"
modulo: "[[Cliente e Endereço]]"
prioridade: Média
alterado: false
entrega: 1
implementacao: completa
lgpd: "[[L4 - Aviso no campo de observação|L4]]"
---
# RF 3.13

o campo de observação do endereço deve exibir um aviso orientando o registro apenas de informações técnicas do imóvel, sem dados de saúde, idade ou outros dados pessoais dos moradores; o sistema não deve ter campos de idade ou saúde;

**Módulo:** [[Cliente e Endereço]]
**Entidades:** [[Observação de Endereço]]

> Origem: ajuste de LGPD [[L4 - Aviso no campo de observação|L4]] ([[LGPD - Visão Geral]]). É o único ajuste de LGPD mantido no MVP, porque já estava implementado: o aviso aparece no formulário de observação do endereço (`Endereco.jsx`).

> Era o RF 3.16 até 28/10/2026; renumerado quando os requisitos da V2 saíram da doc.
