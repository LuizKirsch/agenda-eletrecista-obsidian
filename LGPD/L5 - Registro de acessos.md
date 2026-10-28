---
tags: [lgpd, ajuste]
id: "L5"
tipo: requisito
base: "Marco Civil art. 15; LGPD art. 7º, II"
status: aceito
decisao: "RF V2.1, RF V2.2"
versao: V2
---
# L5 – Registro de acessos (6 meses)

**Base:** Marco Civil art. 15; LGPD art. 7º, II · **Tipo:** requisito novo

## O que a apresentação propõe
Registrar IP, data e hora de cada login dos usuários e apagar os registros após 6 meses.

## Por que não estava no projeto
O sistema não guarda nenhum registro de acesso hoje.

## Onde impacta
- [[Usuários e Acesso]] e [[P2.1 - Autenticar]]
- Domínio — nova entidade/tabela de registro de acesso
- [[API REST]] — gravação no login
- [[Requisitos Não Funcionais]] — possível ajuste no RNF-6

## Análise
- [ ] Validar se entra no MVP ou vai para [[Fora do MVP]]
- [ ] Definir rotina de expurgo dos 6 meses
- [x] Definir número de RF (módulo 2)

## Decisão
Aceito como RF V2.1 e RF V2.2, com P2.5 - Registrar acesso (RN V2.1 e RN V2.2) e a nova entidade Registro de Acesso. Só logins com sucesso; expurgo automático dos registros com mais de 6 meses.

> Origem: apresentação "A LGPD dentro de uma agenda de eletricista" (05/10/2026). Ver [[LGPD - Visão Geral]].

## Texto proposto para a V2

> Retirado da doc em 28/10/2026, junto com os demais RFs e RNs de LGPD; guardado aqui para quando a V2 começar. A numeração é provisória.

**RF V2.1** — o sistema deve registrar o usuário, o IP e a data e hora de cada login realizado com sucesso;

**RF V2.2** — os registros de acesso devem ser apagados automaticamente após 6 meses;

**P2.5 - Registrar acesso**

#### RN V2.1
Cada login realizado com sucesso grava o usuário, o login, o IP e a data e hora do acesso;

#### RN V2.2
Os registros de acesso com mais de 6 meses são apagados automaticamente.

**Tabela `registro_acesso`**

| Nome | Descrição | Tipo | Tamanho | Restrições |
| --- | --- | --- | --- | --- |
| `id` | Identificador único | BIGINT Unsigned | 20 | PK NOT NULL |
| `usuario_id` | Usuário que fez o login | BIGINT Unsigned | 20 | FK usuario, ON DELETE SET NULL |
| `login` | Login usado no acesso | VARCHAR | 60 | NOT NULL |
| `ip` | Endereço IP de origem (IPv4 ou IPv6) | VARCHAR | 45 | NOT NULL |
| `acessado_em` | Data e hora do login | DATETIME |  | NOT NULL, padrão CURRENT_TIMESTAMP |
