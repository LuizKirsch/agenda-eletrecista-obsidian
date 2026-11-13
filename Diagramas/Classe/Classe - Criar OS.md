# Diagrama de classe – Criar OS

Recorte da [[Classe - Geral]] com o que participa de `POST /os` (`os.service.criar`).

```mermaid
classDiagram
direction LR

class OrdemServico {
  -id: number
  -observacao: string
  +renumerarSequencia() void
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

class Usuario {
  -id: number
  -nome: string
  -perfil: Perfil
  -ativo: boolean
  -cor: string
  +podeReceberAtividade() boolean
}

class TipoAtividade {
  -id: number
  -nome: string
  -duracaoPadraoMin: number
  -ativo: boolean
}

class StatusAtividade {
  <<enumeration>>
  AGENDADA
  CONCLUIDA
  CANCELADA
}

OrdemServico "0..*" --> "1" Cliente : de
OrdemServico "0..*" --> "1" Endereco : em
OrdemServico "0..*" --> "1" Usuario : responsável
OrdemServico "1" *-- "1..*" AtividadeOs : composta de
Cliente "1" *-- "0..*" Endereco : possui
AtividadeOs "0..*" --> "1" Usuario : eletricista
AtividadeOs "0..*" --> "0..1" TipoAtividade : do tipo
AtividadeOs ..> StatusAtividade
```

Na criação, toda atividade nasce `AGENDADA`; conflito de horário (`conflitaCom`) só gera aviso (`aviso_conflito`), não bloqueia.
