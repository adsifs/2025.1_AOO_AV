@startuml
!theme mars

class Usuario {
    -id: UUID
    -nomeCompleto: String
    -email: String
    -senhaHash: String
    -tipoLogin: Enum (TRADICIONAL, GOOGLE)
    -permissao: Enum (BASICO, PREMIUM, CORPORATIVO)
    +cadastrar()
    +autenticar()
    +recuperarSenha()
    +editarConta()
    +excluirConta()
}

@enduml
