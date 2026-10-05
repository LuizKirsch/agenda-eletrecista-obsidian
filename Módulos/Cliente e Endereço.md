---
tags: [modulo]
entrega: 1
---
# Cliente e Endereço

Cadastro de clientes e dos endereços vinculados a cada um, com observações específicas por endereço (padrão do quadro elétrico, particularidades de acesso, etc.). O histórico do imóvel é priorizado sobre o histórico do cliente isoladamente, já que o eletricista retorna ao local, não à pessoa. Cada OS é vinculada a um cliente e a um endereço. O telefone identifica o cliente e não pode se repetir. Clientes, endereços e observações podem ser editados, e clientes e endereços só podem ser excluídos quando não houver OS vinculada. A consulta do histórico de OS por endereço ou por cliente fica fora do MVP.

## Entidades
- [[Cliente]]
- [[Endereço]]
- [[Observação de Endereço]]

## Processos e regras de negócio
- [[P3.1 - Cadastrar cliente, endereço e observação]]
- [[P3.2 - Buscar cliente]]
- [[P3.3 - Editar e excluir cliente, endereço e observação]]

## Requisitos funcionais (12)
- [[RF 3.1]] (Alta) — O sistema deve permitir cadastrar cliente com campos mínimos: nome e telefone; o telefone deve ter DDD e 8 ou…
- [[RF 3.2]] (Média) — o cadastro de cliente deve ser rápido, sem campos obrigatórios excessivos
- [[RF 3.3]] (Alta) — o sistema deve permitir vincular N endereços a um mesmo cliente
- [[RF 3.4]] (Alta) — cada endereço deve ser tratado como entidade própria, associada ao cliente
- [[RF 3.5]] (Alta) — o sistema deve permitir registrar uma ou mais observações livres por endereço (ex.: padrão do quadro, cachorro…
- [[RF 3.6]] (Alta) — as observações do endereço devem ficar visíveis ao abrir esse endereço em uma nova OS
- [[RF 3.7]] (Alta) — as observações do endereço devem ser exibidas com a data em que foram registradas, da mais recente para a mais…
- [[RF 3.8]] (Alta) — o sistema deve listar os clientes em ordem alfabética, com busca por parte do nome ou do telefone, sem diferen…
- [[RF 3.9]] (Média) — o sistema deve permitir editar o nome e o telefone do cliente, mantendo as regras do RF 3.1
- [[RF 3.10]] (Média) — o sistema deve permitir editar os dados do endereço e o texto de uma observação; a observação editada mantém a…
- [[RF 3.11]] (Média) — o sistema deve permitir excluir cliente ou endereço, com confirmação, somente quando não houver OS vinculada a…
- [[RF 3.12]] (Média) — o sistema deve permitir excluir uma observação de endereço, com confirmação.

Voltar: [[00 - Visão Geral]]
