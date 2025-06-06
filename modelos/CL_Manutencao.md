@startuml
!theme mars

class Manutencao {
    -id: UUID
    -tipoServico: String
    -data: Date
    -quilometragem: Long
    -oficina: String
    -valor: Double
    -observacoes: String
    -notaFiscalUrl: String
    -autorId: UUID
    -veiculoId: UUID
    +registrar()
    +editar()
    +excluir()
    +lerNotaFiscalOCR()
}

@enduml
