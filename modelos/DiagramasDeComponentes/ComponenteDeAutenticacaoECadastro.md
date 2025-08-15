@startuml
title Módulo de Autenticação e Cadastro - Nexus Marketplace

package "Módulo de Autenticação e Cadastro" {

    [Interface de Usuário] --> [Serviço de Autenticação]
    [Interface de Usuário] --> [Serviço de Cadastro]

    [Serviço de Autenticação] --> [Banco de Dados de Usuários]
    [Serviço de Cadastro] --> [Banco de Dados de Usuários]

    [Serviço de Autenticação] ..> [Serviço de Notificação] : Envia e-mail/SMS de verificação

}

package "Serviços Externos" {
[Serviço de Notificação]
}

database "Banco de Dados de Usuários" as DBUsuarios

@enduml
