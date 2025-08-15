@startuml
' Diagrama de componentes simplificado: Avaliação de produto
skinparam componentStyle rectangle

package "Sistema de Avaliação" {

    [Interface de Usuário] --> [Interface de Avaliações] : envia avaliação
    [Interface de Avaliações] --> [Serviço de Avaliação] : processa avaliação
    [Serviço de Avaliação] --> [Validador de Avaliação] : valida dados
    [Validador de Avaliação] --> [Banco de Dados de Avaliações] : armazena avaliação validada

}

@enduml
