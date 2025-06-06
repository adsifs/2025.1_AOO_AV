@startuml
!theme mars

class Compartilhamento {
    -id: UUID
    -veiculoId: UUID
    -usuarioConvidadoId: UUID
    -permissao: Enum (VISUALIZACAO, EDICAO)
    -codigoConvite: String
    -status: Enum (PENDENTE, ACEITO, REVOGADO)
    +compartilharPorEmail()
    +gerarCodigoConvite()
    +removerAcesso()
    +transferirPropriedade()
}

@enduml
