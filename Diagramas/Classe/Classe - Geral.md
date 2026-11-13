# Diagrama de classe – visão geral do domínio

Métodos representam regras de negócio; na implementação ficam nos services do backend (`server/services/`), não nos models. Atributos seguem o dicionário de dados, com chaves estrangeiras mostradas como relacionamentos.

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
  +atualizar(itens: OrcamentoItem[], autor: Usuario) void
  +recomendarHorarios(data: Date, inicio: Time, eletricista: Usuario) Horario[]
  +aceitar(horarios: Horario[], eletricista: Usuario, confirmarConflito: boolean) OrdemServico
  +recusar() void
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

class OrcamentoVersao {
  -id: number
  -numero: number
  -snapshot: string
  -criadoEm: Date
}

class Horario {
  <<dataType>>
  -data: Date
  -horaInicio: Time
  -eletricista: Usuario
}

class OrdemServico {
  -id: number
  -observacao: string
  +somenteLeitura() boolean
  +atualizar(atividades: AtividadeOs[]) void
  +deslocar(referencia: AtividadeOs, data: Date, inicio: Time) void
  +concluir() void
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
  +remarcar(data: Date, inicio: Time, fim: Time) void
  +alterarStatus(novo: StatusAtividade) void
  +podeExcluir() boolean
}

class Cliente {
  -id: number
  -nome: string
  -telefone: string
  -criadoEm: Date
  +telefoneValido() boolean
  +podeExcluir() boolean
}

class Endereco {
  -id: number
  -identificacao: string
  -logradouro: string
  -numero: string
  -complemento: string
  -bairro: string
  -cidade: string
  -pontoReferencia: string
  +pertenceA(cliente: Cliente) boolean
  +podeExcluir() boolean
}

class EnderecoObservacao {
  -id: number
  -texto: string
  -criadoEm: Date
}

class TipoAtividade {
  -id: number
  -nome: string
  -duracaoPadraoMin: number
  -valorPadrao: number
  -ativo: boolean
  +quantidadeDeUso() number
  +podeDesativar() boolean
}

class Usuario {
  -id: number
  -nome: string
  -login: string
  -senhaHash: string
  -perfil: Perfil
  -ativo: boolean
  -cor: string
  +conferirSenha(senha: string) boolean
  +podeGerenciarUsuarios() boolean
  +podeReceberAtividade() boolean
}

class StatusOrcamento {
  <<enumeration>>
  PENDENTE
  ACEITO
  RECUSADO
}

class StatusAtividade {
  <<enumeration>>
  AGENDADA
  CONCLUIDA
  CANCELADA
}

class Perfil {
  <<enumeration>>
  ELETRICISTA
  SECRETARIA
}

Orcamento "0..*" --> "1" Cliente : de
Orcamento "0..*" --> "1" Endereco : em
Orcamento "1" *-- "1..*" OrcamentoItem : composto de
Orcamento "1" *-- "0..*" OrcamentoVersao : versões
Orcamento "0..1" --> "0..1" OrdemServico : gera
Orcamento ..> StatusOrcamento
Orcamento ..> Horario
OrcamentoItem "0..*" --> "0..1" TipoAtividade : do catálogo
OrcamentoVersao "0..*" --> "0..1" Usuario : salva por

OrdemServico "0..*" --> "1" Cliente : de
OrdemServico "0..*" --> "1" Endereco : em
OrdemServico "0..*" --> "1" Usuario : responsável
OrdemServico "1" *-- "1..*" AtividadeOs : composta de
AtividadeOs "0..*" --> "0..1" TipoAtividade : do tipo
AtividadeOs "0..*" --> "1" Usuario : eletricista
AtividadeOs ..> StatusAtividade

Cliente "1" *-- "0..*" Endereco : possui
Endereco "1" *-- "0..*" EnderecoObservacao : tem
Usuario ..> Perfil
```

## Onde cada método está no código

| Método | Implementação | Regra |
|---|---|---|
| `Orcamento.calcularTotal()` | `orcamento.service` → `totalDe` | RN 48 |
| `Orcamento.podeEditar()` | `orcamento.service` → `garantirPendente` | RN 54 |
| `Orcamento.atualizar()` | `orcamento.service.atualizar` (grava `OrcamentoVersao` antes) | RF 4.18 |
| `Orcamento.recomendarHorarios()` | `orcamento.service.recomendarHorarios` → `recomendacao.recomendar` | RF 4.19, RN 67 |
| `Orcamento.aceitar()` | `orcamento.service.aceitar` (conflito sem confirmação → 409) | RN 51, RN 68 |
| `Orcamento.recusar()` | `orcamento.service.recusar` | — |
| `OrcamentoItem.subtotal()` / `ehAvulso()` / `gerarAtividade()` | dentro de `totalDe` e `aceitar` | — |
| `OrdemServico.somenteLeitura()` | `os.service.atualizar` (sem atividade agendada → 409) | RN 9 |
| `OrdemServico.atualizar()` | `os.service.atualizar` (cria, altera e remove atividades) | P6.4, P6.8 |
| `OrdemServico.deslocar()` | `os.service.deslocar` | P6.2 |
| `OrdemServico.concluir()` | `os.service.concluir` | P6.6 |
| `OrdemServico.renumerarSequencia()` | `os.service.atualizar` / `excluirAtividade` | RN 35 |
| `AtividadeOs.conflitaCom()` | `agenda.service.idsEmConflito` | RN 10 |
| `AtividadeOs.remarcar()` | `os.service.remarcarAtividade` | P6.3 |
| `AtividadeOs.alterarStatus()` | `os.service.alterarStatus` (agendada → concluída/cancelada) | P6.6 |
| `AtividadeOs.podeExcluir()` | `os.service.excluirAtividade` (só concluída/cancelada) | RN 14, RN 15 |
| `Cliente.telefoneValido()` | `cliente.service` → `validarTelefone` (DDD + 8/9 dígitos, único) | — |
| `Cliente.podeExcluir()` | `cliente.service.excluir` (bloqueia se houver OS) | — |
| `Endereco.pertenceA()` | `os.service.validarClienteEndereco` | RN 34 |
| `Endereco.podeExcluir()` | `endereco.service.excluir` (bloqueia se houver OS) | — |
| `TipoAtividade.quantidadeDeUso()` | `tipoAtividade.service.contarUso` | — |
| `TipoAtividade.podeDesativar()` | `tipoAtividade.service` → `garantirOutroAtivo` (não desativa o último ativo) | RF 5.6 |
| `Usuario.conferirSenha()` | `auth.service.entrar` (bcrypt) | P2.1 |
| `Usuario.podeGerenciarUsuarios()` | middleware `somenteSecretaria` | — |
| `Usuario.podeReceberAtividade()` | `os.service.validarEletricistas` (perfil eletricista e ativo) | RN 63 |

O fim sugerido da atividade (duração padrão do tipo, RN 2) é calculado só no front (`fimPara` em `client/src/agenda/OsForm.jsx`), por isso não aparece como método.
