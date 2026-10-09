---
tags: [lgpd, ajuste]
id: "L4"
tipo: requisito
base: "LGPD art. 6º, III; art. 11; art. 14"
status: aceito
decisao: "RF 3.16"
---
# L4 – Aviso no campo de observação

**Base:** LGPD art. 6º, III; art. 11; art. 14 · **Tipo:** requisito novo (interface)

## O que a apresentação propõe
Exibir no campo de observação do endereço um aviso pedindo só informação técnica do imóvel, e não criar campo para idade ou saúde.

## Por que não estava no projeto
A observação é texto livre. Na entrevista, o eletricista contou que pergunta se há adolescentes na casa; anotado, vira dado de adolescente (art. 14). Um morador com aparelho médico vira dado de saúde, sensível (art. 11), que não aceita legítimo interesse como base.

## Onde impacta
- [[Observação de Endereço]]
- [[P3.1 - Cadastrar cliente, endereço e observação]] e [[P3.3 - Editar e excluir cliente, endereço e observação]]
- [[Frontend]] — texto de apoio no campo

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir o texto do aviso
- [ ] Validar com o Edson se o aviso atrapalha o uso em campo

## Decisão
Aceito como [[RF 3.16]]. Texto sugerido para o aviso: "Anote só informações técnicas do imóvel (quadro, acesso, fiação). Não registre dados de saúde, idade ou outros dados pessoais dos moradores."

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].
