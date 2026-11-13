---
tags: [requisito]
id: "RF 4.21"
modulo: "[[Orçamento (módulo)]]"
prioridade: Baixa
alterado: true
entrega: 3
implementacao: pendente
---
# RF 4.21

na recomendação de horários do aceite ([[RF 4.19]]), o sistema deve considerar o tempo de deslocamento do eletricista entre o endereço de uma atividade já agendada e o da nova atividade, usando a geolocalização (latitude e longitude) salva no [[Endereço]] (decisão do projeto);

**Módulo:** [[Orçamento (módulo)|Orçamento]]
**Entidades:** [[Endereço]], [[Atividade da OS]], [[Orçamento]]
**Regras:** [[P4.2 - Aceitar ou recusar orçamento]] (estende a [[P4.2 - Aceitar ou recusar orçamento#RN 67|RN 67]])

> Origem: ideia do Luiz (06/11/2026). Em análise: ainda não virou regra, nem foi para o banco ou para o código.
> Fora da documentação técnica da V1 do sistema (decisão de 11/11/2026).

## Proposta (rascunho)
- **Geocodificação:** salvar `latitude` e `longitude` no [[Endereço]] uma vez, ao cadastrar ou editar.
  - Nominatim (OpenStreetMap): grátis, sem chave, limite de 1 requisição por segundo (suficiente para cadastro manual).
  - Google Geocoding: mais preciso, mas exige chave de API e cobrança ativa.
- **Tempo de deslocamento:** distância em linha reta (Haversine) ÷ velocidade média (~30 km/h) × fator de 1,3 a 1,4 para as ruas. Conta local, sem API.
- **No first-fit** (`services/recomendacao.js`): em vez de começar em `teto15(o.fim)`, começar em `teto15(o.fim + deslocamento)`, e exigir que sobre tempo para chegar à atividade seguinte. A função continua pura: `ocupadosPor` passa a devolver as coordenadas junto com `ini`/`fim`.
- **Sem coordenada** (geocodificação falhou ou endereço antigo): deslocamento 0, ou seja, o comportamento atual.
- As atividades de uma mesma OS ficam no mesmo endereço, então o deslocamento só conta entre OS diferentes.

## Fora do escopo
- Distance Matrix do Google a cada recálculo: a tela recalcula com debounce, então cada recálculo vira uma chamada paga e lenta.
- Reordenar atividades para minimizar o trajeto (otimização de rota).
