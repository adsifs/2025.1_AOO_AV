@startuml
title Mediação do Administrador - Nexus Marketplace

package "Módulo de Mediação de Disputas" {

    [Interface de Administrador] --> [Serviço de Análise de Disputas] : Consulta detalhes e evidências
    [Serviço de Análise de Disputas] --> [Banco de Dados de Disputas] : Obtém dados da disputa

    [Serviço de Análise de Disputas] --> [Serviço de Tomada de Decisão] : Envia informações para decisão
    [Serviço de Tomada de Decisão] --> [Banco de Dados de Disputas] : Registra decisão e atualiza status

    [Serviço de Tomada de Decisão] --> [Serviço de Notificação] : Informa partes envolvidas sobre a decisão

}

package "Serviços Externos" {
[Serviço de Notificação]
}

database "Banco de Dados de Disputas" as DBDisputas

@enduml
