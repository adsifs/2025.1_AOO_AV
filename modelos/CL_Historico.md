@startuml
!theme mars

class Historico {
    -id: UUID
    -dataRegistro: Date
    -tipoRegistro: Enum (MANUTENCAO, DESPESA, ATUALIZACAO_KM, CHECKLIST)
    -detalhes: String
    -veiculoId: UUID
    -autorId: UUID
    +consultar()
    +filtrar()
    +gerarRelatorioPDF()
}

@enduml
