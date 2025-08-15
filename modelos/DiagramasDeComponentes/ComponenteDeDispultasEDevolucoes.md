@startuml
title Módulo de Disputas e Devoluções - Nexus Marketplace

package "Módulo de Disputas e Devoluções" {

[Interface de Usuário] --> [Serviço de Registro de Disputa] : Usuário registra conflito ou problema
[Interface de Usuário] --> [Serviço de Solicitação de Devolução] : Usuário solicita devolução de produto
[Interface de Usuário] --> [Serviço de Acompanhamento] : Usuário acompanha status de disputa ou devolução

[Serviço de Registro de Disputa] --> [Banco de Dados de Disputas] : Salva detalhes da disputa
[Serviço de Solicitação de Devolução] --> [Banco de Dados de Devoluções] : Salva detalhes da devolução

[Serviço de Mediação do Administrador] --> [Banco de Dados de Disputas] : Consulta e atualiza status da disputa
[Serviço de Mediação do Administrador] --> [Serviço de Notificação] : Notifica usuário, vendedor ou comprador

[Serviço de Processamento de Devolução] --> [Banco de Dados de Devoluções] : Atualiza status da devolução
[Serviço de Processamento de Devolução] --> [Serviço de Notificação] : Notifica usuário e vendedor

[Serviço de Acompanhamento] --> [Banco de Dados de Disputas] : Lê informações de disputas
[Serviço de Acompanhamento] --> [Banco de Dados de Devoluções] : Lê informações de devoluções
}

package "Serviços Externos" {
[Serviço de Notificação]
}

database "Banco de Dados de Disputas" as DBDisputas
database "Banco de Dados de Devoluções" as DBDevolucoes

@enduml
