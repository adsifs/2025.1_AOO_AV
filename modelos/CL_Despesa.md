@startuml
!theme mars

class Despesa {
    -id: UUID
    -tipo: String
    -data: Date
    -valor: Double
    -descricao: String
    -categoria: String
    -comprovanteUrl: String
    -veiculoId: UUID
    -autorId: UUID
    +registrar()
    +editar()
    +excluir()
}

@enduml
