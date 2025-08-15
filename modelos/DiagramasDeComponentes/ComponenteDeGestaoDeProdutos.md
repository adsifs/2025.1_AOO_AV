@startuml
title Módulo de Gestão de Produtos - Nexus Marketplace

package "Módulo de Gestão de Produtos" {

    [Interface de Usuário] --> [Serviço de Publicação de Produto]
    [Interface de Usuário] --> [Serviço de Atualização de Produto]

    [Serviço de Publicação de Produto] --> [Serviço de Moderação de Produto]
    [Serviço de Atualização de Produto] --> [Serviço de Moderação de Produto]

    [Serviço de Moderação de Produto] --> [Banco de Dados de Produtos]
    [Serviço de Moderação de Produto] ..> [Serviço de Notificação] : Notifica vendedor/aprovador

}

package "Serviços Externos" {
[Serviço de Notificação]
}

database "Banco de Dados de Produtos" as DBProdutos

@enduml
