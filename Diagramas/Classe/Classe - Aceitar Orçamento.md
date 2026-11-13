# Diagrama de classe – Aceitar orçamento

Recorte da [[Classe - Geral]] com o que participa de `POST /orcamentos/:id/aceitar` (`orcamento.service.aceitar`).

```mermaid
classDiagram
direction LR

class Orcamento {
  -id: number
  -status: StatusOrcamento
  -observacao: string
  -criadoEm: Date
  +calcularTotal() number
  +podeEditar() boolean
  +recomendarHorarios(data: Date, inicio: Time, eletricista: Usuario) Horario[]
  +aceitar(horarios: Horario[], eletricista: Usuario, confirmarConflito: boolean) OrdemServico
}

class OrcamentoItem {
  -id: number
  -descricao: string
  -quantidade: number
  -valorUnitario: number
  -duracaoMin: number
  -sequencia: number
  +subtotal() number
  +ehAvulso() boolean
  +gerarAtividade(horario: Horario) AtividadeOs
}

class Horario {
  <<dataType>>
  -data: Date
  -horaInicio: Time
  -eletricista: Usuario
}

class Cliente {
  -id: number
  -nome: string
  -telefone: string
}

class Endereco {
  -id: number
  -logradouro: string
  -cidade: string
  +pertenceA(cliente: Cliente) boolean
}

class TipoAtividade {
  -id: number
  -nome: string
  -duracaoPadraoMin: number
  -valorPadrao: number
  -ativo: boolean
}

class OrdemServico {
  -id: number
  -observacao: string
}

class AtividadeOs {
  -id: number
  -descricao: string
  -sequencia: number
  -data: Date
  -horaInicio: Time
  -horaFim: Time
  -status: StatusAtividade
  +conflitaCom(outra: AtividadeOs) boolean
}

class Usuario {
  -id: number
  -nome: string
  -perfil: Perfil
  -ativo: boolean
  -cor: string
  +podeReceberAtividade() boolean
}

class StatusOrcamento {
  <<enumeration>>
  PENDENTE
  ACEITO
  RECUSADO
}

Orcamento "0..*" --> "1" Cliente : de
Orcamento "0..*" --> "1" Endereco : em
Orcamento "1" *-- "1..*" OrcamentoItem : composto de
Orcamento "0..1" --> "0..1" OrdemServico : gera
Orcamento ..> StatusOrcamento
Orcamento ..> Horario
Cliente "1" *-- "0..*" Endereco : possui
OrcamentoItem "0..*" --> "0..1" TipoAtividade : do catálogo
OrdemServico "0..*" --> "1" Usuario : responsável
OrdemServico "1" *-- "1..*" AtividadeOs : composta de
AtividadeOs "0..*" --> "1" Usuario : eletricista
```

`aceitar` gera uma `AtividadeOs` por item (`gerarAtividade`). Se houver conflito e `confirmarConflito` for falso, o aceite é recusado (409) e nada é gravado; com confirmação, grava e devolve o aviso (RN 68).
